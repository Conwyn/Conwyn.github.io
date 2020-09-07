# Homomorphic Encryption

Homomorphic Encryption is a method to encrypt data but allows addition and multiplication to be performed on the encrypted data.

Integer only is described in this excellent article:
https://blog.openmined.org/build-an-homomorphic-encryption-scheme-from-scratch-with-python/


Real numbers are partially described in this series of articles:
https://towardsdatascience.com/homomorphic-encryption-intro-part-3-encoding-and-decoding-in-ckks-69a5e281fee

The original paper is:
https://eprint.iacr.org/2016/421.pdf 

The common element is the Ring Learning with Errors and Polynomial quotient Ring.
So what is a ring.
We have a set of non-repeating elements and an operator called addition. So A + B  = C where C is an element
We have a zero element so A + 0 = A
We have inverse so A + B = 0 means B is the oposite of A.
Consider clock time which has a range 0 to 23.  1+2 = 3 23+3 = 2; 1+0 =1. 23+1 = 0

Next we have a second operator multiply.  3 * 6 = 18 and 6 * 6 = (36-24) = 12. 1 * 6 = 6 
So add (1+2) +3 = 1 + (2+3) and (2 * 3) * 4 = 2 * (3 * 4) and you have a ring.

Moving from number to Polynomials. A polynomial is A0 + A1*X + A2*X*X + ...
So consider (A0 + A1 * X) +  (B0 + B1 *  X) = (A0+B0) + (A1+B1)* X 
and (A0 + A1 * X) * ( B0 + B1 * X) = (A0 * B0) + (A0 * B1 + (A1 * B0)*X  +(B0 * B1) * X * X

Now the polynomials will get larger so we divide by another ploymomial and keep the remainder.
This is called a polynomial quotient ring.

The first process is to generate a private and public key (tuple of polynomials).
The plain text integer becomes a polynomial M + 0 * X + 0 * X * X .... and then encrypted.
The magic is the key generation includes a random number 

#
CKKS is slightly more complex.
It takes real numbers and encodes them into a polynomial. 
-1 has roots so if our message is m1,m2,m3,m4 then we need a polynomial of the order  X^8 where the first, third, fifth and seventh roots 
when evaluated by the polynomial has the value m1,m2,m3,m4.
The polynomial is then encrypted similar to above. The only addition is mutiplication has a special key called the evaluation key.






