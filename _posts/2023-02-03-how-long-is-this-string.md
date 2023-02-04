---
layout: post
title: How long is this string ?
date: 2023-02-03 22:51 +0100
---
For the last few months I have been working in a research center.One of the problems most of us in the tech industry face is hiring the right people to join the team.

One of the questions we ask the candidates is to calculate the length of a string in c.The answer is pretty simple however many candidates are not able to handle it.


Here is the solution to the problem.
We start from the first character in the string and increment a counter as we read the next character until we come across the special null character ('\0').The length of the string is the counter.

This solution is good enough for the interview however if we look at the standard library for c we see different implementations for it.
The LLVM libc has the following implementation

```c
size_t strlen(const char *src){
  size_t length;
  for (length = 0; *src; ++src, ++length);
  return length;
}
```
However we can also see that there is another implementation present in the standard which is marked as unsafe.

```c
template <typename Word>
inline size_t unsafe_strlen(const char *src) {
  const char *char_ptr = src;
  // Step 1: read 1 byte at a time to align to block size
  for (; reinterpret_cast<uintptr_t>(char_ptr) % sizeof(Word) != 0;
       ++char_ptr) {
    if (*char_ptr == '\0')
      return char_ptr - src;
  }
  // Step 2: read blocks
  for (const Word *block_ptr = reinterpret_cast<const Word *>(char_ptr);
       !has_zeroes<Word>(*block_ptr); ++block_ptr) {
    char_ptr = reinterpret_cast<const char *>(block_ptr);
  }
  // Step 3: find the zero in the block
  for (; *char_ptr != '\0'; ++char_ptr) {
    ;
  }
  return char_ptr - src;
}

template <typename Word> constexpr Word repeat_byte(Word byte) {
  constexpr size_t BITS_IN_BYTE = 8;
  constexpr size_t BYTE_MASK = 0xff;
  Word result = 0;
  byte = byte & BYTE_MASK;
  for (size_t i = 0; i < sizeof(Word); ++i)
    result = (result << BITS_IN_BYTE) | byte;
  return result;
}

template <typename Word> constexpr bool has_zeroes(Word block) {
  constexpr Word LOW_BITS = repeat_byte<Word>(0x01);
  constexpr Word HIGH_BITS = repeat_byte<Word>(0x80);
  Word subtracted = block - LOW_BITS;
  Word inverted = ~block;
  return (subtracted & inverted & HIGH_BITS) != 0;
}
```

Here's the flow for the algorithm
1. Align the position of the current pointer to be aligned by the size of the datatype
2. Then read the data in chunks of size of the datatype and check if the there are any zeros.
3. If there are zeros present break out and increment the pointer position until the termination character is reached.
4. Now we have the size which is the difference between the original pointer position and the current pointer position.

Now that seems like a lot of code to check if the next character is the null termination character.
The templates however would let us apply strlen on character arrays as well as custom types like char32_t, char16_t which are used for UTF-32 and UTF-16.

This code is pretty complex where you could just replace it with multiple if conditions based on the size of the datatype.If you think about it with more scrutiny you will realize that the we would have 4 checks per loop which is a lot of branches and this could end up slowing down our program.

This is exactly what the GNU libc have implemented.
```c
size_t strlen (const char *str)
{
  const char *char_ptr;
  const unsigned long int *longword_ptr;
  unsigned long int longword, himagic, lomagic;

  /* Handle the first few characters by reading one character at a time.
     Do this until CHAR_PTR is aligned on a longword boundary.  */
  for (char_ptr = str; ((unsigned long int) char_ptr
			& (sizeof (longword) - 1)) != 0;
       ++char_ptr)
    if (*char_ptr == '\0')
      return char_ptr - str;

  /* All these elucidatory comments refer to 4-byte longwords,
     but the theory applies equally well to 8-byte longwords.  */

  longword_ptr = (unsigned long int *) char_ptr;

  /* Computing (longword - lomagic) sets the high bit of any corresponding
     byte that is either zero or greater than 0x80.  The latter case can be
     filtered out by computing (~longword & himagic).  The final result
     will always be non-zero if one of the bytes of longword is zero.  */
  himagic = 0x80808080L;
  lomagic = 0x01010101L;
  if (sizeof (longword) > 4)
    {
      /* 64-bit version of the magic.  */
      /* Do the shift in two steps to avoid a warning if long has 32 bits.  */
      himagic = ((himagic << 16) << 16) | himagic;
      lomagic = ((lomagic << 16) << 16) | lomagic;
    }
  if (sizeof (longword) > 8)
    abort ();

  /* Instead of the traditional loop which tests each character,
     we will test a longword at a time.  The tricky part is testing
     if *any of the four* bytes in the longword in question are zero.  */
  for (;;)
    {
      longword = *longword_ptr++;

      if (((longword - lomagic) & ~longword & himagic) != 0)
	{
	  /* Which of the bytes was the zero?  */

	  const char *cp = (const char *) (longword_ptr - 1);

	  if (cp[0] == 0)
	    return cp - str;
	  if (cp[1] == 0)
	    return cp - str + 1;
	  if (cp[2] == 0)
	    return cp - str + 2;
	  if (cp[3] == 0)
	    return cp - str + 3;
	  if (sizeof (longword) > 4)
	    {
	      if (cp[4] == 0)
		return cp - str + 4;
	      if (cp[5] == 0)
		return cp - str + 5;
	      if (cp[6] == 0)
		return cp - str + 6;
	      if (cp[7] == 0)
		return cp - str + 7;
	    }
	}
    }
}
```

As I mentioned earlier with more branches you would expect the IPC for the program to drop.Lets look at compiler explorer to see if the compiler can help optimize away some of the unwanted instruction.

Running the both the functions on quick bench I didnt see a big difference in the performance of both the functions.In real world applications this tiny comparison would not really make a big difference in the runtime of the program.

`However if we look at the block read function in both the functions the GNU version performs the reads in block size of 4 bytes by default whereas the LLVM libc version depends on the datatype that you pass as the template parameter.`




