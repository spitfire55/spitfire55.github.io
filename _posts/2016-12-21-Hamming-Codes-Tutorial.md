---
layout: post
title: Hamming Codes Tutorial
description: A brief introduction to using parity bits for memory errors
---

[R.W. Hamming]("https://en.wikipedia.org/wiki/Richard_Hamming") designed a very simple but effective error-correcting code to detect one-bit and two-bit errors, and fix one-bit errors. Hamming codes are limited to certain kinds of data that has low error rates, such as computer memory (RAM, caches, etc.). The following is a simple explanation of how Hamming codes work.

1. Parity bits are inserted within data at 2<sup>n</sup> indices (1,2,4,8,16,etc.). Data bits are shifted to the right accordingly. 

2. The parity bit's location reflects where the parity bit is used.  
    a. Parity bit 1 checks 1,3,5,7,9,etc. (check 1, skip 1)  
    b. Parity bit 2 checks 2,3,6,7,10,11,etc. (check 2, skip 2)  
    c. Parity bit 4 checks 4,5,6,7,12,13,14,15,etc. (check 4, skip 4)  
    d. Pattern continues for parity bit 8, 16, 32, etc.  
___Note: The pattern includes the parity bit itself___

3. Each bit checked reflects what value the parity bit should hold. For example, if the data sequence is 1010, and parity bits are placed at indices 1, 2, and 4, then the entire sequence of bits would be the following:  
<pre>
<center><b>1 0</b> 1 <b>1</b> 0 1 0</center>
<center><b>1 2</b> 3 <b>4</b> 5 6 7</center>
</pre>

Parity bit 1 checks the data bits at index 3 and 5. Since the sum of these two data bits is an odd value, the first parity bit should be 1. For parity bit 2, we check bits 3 and 6. The sum of these two bits is 2, an even value, so we set parity bit 2 to 0. Finally, parity bit 4 will be checking indices 5 through 7. The sum of these three bits is odd, so the 4<sup>th</sup> parity bit will be set to 1. 

This is easy to implement, but how does it detect errors? Hamming codes have the unique property of being able to detect and fix one-bit errors. This is because one data bit affects at least two parity bits. If one data bit is flipped due to noise on the data bus, then the parity bits can be checked to see which bit is affected.  

For example, here is a stream of data with parity bits placed in 2<sup>n</sup> indices.  
<pre>
<center>0 1 0 0 0 1 0 0 1 1  0  1 </center>
<center>1 2 3 4 5 6 7 8 9 10 11 12</center>
</pre>

If we check the parity bits for accuracy (I'll skip the process above and just ask you trust me), we will see that three parity bits are incorrect: 1, 2, and 8. We know that parity bit 1 checks data bits 3, 5, 7, 9, and 11. Parity bit 2 checks data bits 3, 6, 7, 10, and 11. Parity bit 8 checks data bits 9, 10, 11, and 12. Of these three lists of data bits, the single common index is 11. This means the data bit at index 11 needs to be flipped back to a 1 in order for all the parity values to be correct.  

Notice how this will only work if a single bit is flipped. If more than one bit is flipped, we will not always be able to know if something is wrong. Even if we can detect it (in most cases we can with Hamming codes), we have no way of knowing which individual data bits need to be flipped. Thus, Hamming codes should only be used in hardware that has low error rates, like RAM traveling on the data bus from memory to the CPU.  

Earlier I also stated that Hamming codes can also detect two-bit errors but not fix them. The way to add this detection capability is simply prepend the entire stream of bits with another parity bit. This parity bit reflects the parity of all data bits in the stream. So, in the example above with a 12 bit data stream, let's assume we implemented this additional parity bit. If the bit was zero, and we fix index 11, we know that index 11 was the only bit that flipped. However, if the parity bit was 1, we know that some other bit was flipped, too, since this parity bit is now incorrect.

I hope this simple tutorial covered Hamming codes well. More information can be found on the [Wikipedia page]("https://en.wikipedia.org/wiki/Hamming_code"). Happy coding!


