---
layout: post
title: Writing a simple cpp allocator
date: 2023-04-04 10:19 +0200
---
Last year I had joined BSC to work on my master's thesis, my goal was to replace the standard cpp allocator with a custom allocator which would allocate to heterogenous memory systems automatically.

It was the first time for me to write a custom allocator in cpp.Here is how I did it.
```
#include <iostream>

using namespace std;

template<class T>
struct TestAllocator {
    typedef T value_type;

    TestAllocator() noexcept;
    
    template<class U>
    TestAllocator(const TestAllocator <U> &) noexcept {}

    template<class U>
    bool operator==(const TestAllocator<U> &) const noexcept {
        return true;
    }

    template<class U>
    bool operator!=(const TestAllocator<U> &) const noexcept {
        return false;
    }

    T *allocate(const size_t n) const;

    void deallocate(T *const p, size_t) const noexcept;
};

template<class T>
T *TestAllocator<T>::allocate(const size_t n) const {
    if (n == 0) {
        return nullptr;
    }
    if (n > static_cast<size_t>(-1) / sizeof(T)) {
        throw std::bad_array_new_length();
    }

    void *baseptr = malloc(n);
    if (!baseptr){
        throw std::bad_alloc();
    }

    return static_cast<T *>(baseptr);
}

template<class T>
void TestAllocator<T>::deallocate(T *const p, size_t) const noexcept {
    free(p);
}

template<class T>
TestAllocator<T>::TestAllocator() noexcept {
}
```
One of the issues I faced was not declaring `typedef T value_type` for the class template.The error message that would be returned by the compiler was not easy to comprehend
``` 
/usr/include/c++/11/bits/stl_vector.h:1582:75: error: ‘_M_get_Tp_allocator’ was not declared in this scope; did you mean ‘get_allocator’?
 1582 |             = this->_M_allocate(_S_check_init_len(__n, _M_get_Tp_allocator()));
      |                                                        ~~~~~~~~~~~~~~~~~~~^~
      |                                                        get_allocator
/usr/include/c++/11/bits/stl_vector.h:1583:25: error: ‘struct std::_Vector_base<int, TestAllocator<int> >::_Vector_impl’ has no member named ‘_M_end_of_storage’
 1583 |           this->_M_impl._M_end_of_storage = this->_M_impl._M_start + __n;
      |           ~~~~~~~~~~~~~~^~~~~~~~~~~~~~~~~
/usr/include/c++/11/bits/stl_vector.h:1583:59: error: ‘struct std::_Vector_base<int, TestAllocator<int> >::_Vector_impl’ has no member named ‘_M_start’
 1583 |           this->_M_impl._M_end_of_storage = this->_M_impl._M_start + __n;
      |                                             ~~~~~~~~~~~~~~^~~~~~~~
/usr/include/c++/11/bits/stl_vector.h:1584:25: error: ‘struct std::_Vector_base<int, TestAllocator<int> >::_Vector_impl’ has no member named ‘_M_finish’
 1584 |           this->_M_impl._M_finish =
      |           ~~~~~~~~~~~~~~^~~~~~~~~
/usr/include/c++/11/bits/stl_vector.h:1586:55: error: ‘struct std::_Vector_base<int, TestAllocator<int> >::_Vector_impl’ has no member named ‘_M_start’
 1586 |                                         this->_M_impl._M_start,
 ```
 Looking at the `stl_vector.h` file we come across the following which gave me the hint that we are expecting the missing type information.
#### **`/usr/include/c++/11/bits/stl_vector.h`**
 ``` 
   128       struct _Vector_impl
   129           : public _Tp_alloc_type, public _Vector_impl_data
   ...
   ...
   246       private:
   247         _Vector_impl& _M_impl;
   ...
   279       const _Tp_alloc_type&
   280       _M_get_Tp_allocator() const _GLIBCXX_NOEXCEPT
   281       { return this->_M_impl; }
   ...
   293       _Vector_base(const allocator_type& __a) _GLIBCXX_NOEXCEPT
   294       : _M_impl(__a) { }
   ...
   397       __glibcxx_class_requires2(_Tp, _Alloc_value_type, _SameTypeConcept)
 ```

Now we can use it to replace any standard library class.
```
int main() {
    vector<int, TestAllocator<int>> test { 10, 10, 10,10,10,10,10 };
    for(int i: test){
        cout << i << endl;
    }
    return 0;
}
```
