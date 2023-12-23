---
layout: post
title: IR replacement with LLVM passes
date: 2023-12-23 00:58 +0100
---
For the last few weeks I have been trying to understand how graphics code (shaders) are compiled in to assembly that the graphics cards understand.This was part of open source contribution to the RISCV Graphics group.The team at the graphics group were looking for people who would be willing to work on the different stacks of the RISCV graphics stack.Currently the project I am working on is at a very early stage.

The goal of the project is to convert SPIRV graphics code to RISCV assembly.SPIRV is a widely used IR and it supported by most common shading languages like HLSL and GLSL.The khronous group wants to make this IR a universal IR to also support more than just graphics related operations.

Since was already some on going work by the LLVM team to convert SPIRV to LLVM, we decided to take a look at it, however it didnt support GLSL compiled SPIRV.We then decided to look at AMDs compiler which ended up supporting it.

My first go was writing a quick transformation pass and added it at the end of the first stage of the compiler.
Here is how I implemented the Pass.

```
class SpirvSamplerLowering : public llvm::PassInfoMixin<SpirvSamplerLowering> {
public:
  llvm::PreservedAnalyses run(llvm::Function &function, llvm::FunctionAnalysisManager &analysisManager) {
    LLVM_DEBUG(dbgs() << "Run the pass Spirv-Sampler-Lower\n");
    m_builder = std::make_unique<IRBuilder<>>(function.getContext());
    for (auto &bb : function) {
      for (auto &inst : bb) {
        if (auto *ci = llvm::dyn_cast<llvm::CallInst>(&inst)) {
          if (ci->getCalledFunction()->getName().starts_with("lgc.create.image.sample")) {
            IRBuilder<> Builder(ci);
            std::vector<Value *> Args(ci->arg_begin(), ci->arg_end());
            llvm::FunctionCallee newCallee = function.getParent()->getOrInsertFunction("llvm.riscv.image.sample", ci->getFunctionType());
            llvm::CallInst *newCallInst = Builder.CreateCall(newCallee, Args);
            ci->replaceAllUsesWith(newCallInst);
            m_instsToErase.push_back(ci);
          }
          LLVM_DEBUG(dbgs() << ci->getCalledFunction()->getName() << "\n");
        }
      }
    }
  
    const bool changed = !m_instsToErase.empty();
    for (Instruction *const inst : m_instsToErase) {
      inst->eraseFromParent();
    }
    m_instsToErase.clear();
  
    return changed ? PreservedAnalyses::none() : PreservedAnalyses::all();
  }

    const bool changed = !m_instsToErase.empty();
    for (Instruction *const inst : m_instsToErase) {
      inst->eraseFromParent();
    }
    m_instsToErase.clear();

    return changed ? PreservedAnalyses::none() : PreservedAnalyses::all();
  }

  static llvm::StringRef name() { return "Lower LLPC sampler to LLVM sampler IR"; }

private:
  std::unique_ptr<llvm::IRBuilder<>> m_builder;
  llvm::SmallVector<llvm::Instruction *, 8> m_instsToErase;
}
```

The run function executes when it run the pass.We then iterate over the function and its basic blocks to find the instruction that calls the lgc instrinsic we are trying to replace.
Once we have a reference to the intrinsic we copy the arguments passed to the instrinsic and create a new instruction with the passed arguments.We then store the reference to the instruction in a vector to be delted later.

Writing this pass was pretty simple and it mostly felt like a fancy regex on the IR.
