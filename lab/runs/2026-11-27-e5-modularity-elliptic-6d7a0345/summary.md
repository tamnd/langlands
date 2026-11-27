# 2026-11-27-e5-modularity-elliptic-6d7a0345

For each isogeny class of elliptic curves over Q of conductor N <= 1000 in the Cremona database, are the a_p of the curve, from point counts mod p, equal to the a_p of the newform of weight 2 and level N in the aplist of the database, at each prime of the aplist, and for which N do these primes reach the Sturm bound floor(N prod_{p | N} (1 + 1/p) / 6)?

Result: agrees: for each of the 2463 classes the a_p of the curve agree with the aplist at all its primes, 61944 in total; for 643 classes these primes reach the Sturm bound, and for the other 1820 the check is partial.

## The data

Source: J. E. Cremona, the Cremona database of elliptic curves, the repository ecdata, https://github.com/JohnCremona/ecdata, read on 2026-11-27 with gh api and the header Accept application/vnd.github.raw, at the commit 6fedd3ab463a70e52061ebc0b04832ad19fd2e01.

Licence: The Artistic License 2.0. The README says that the data is available under TheArtistic License 2.0, and LICENSE is the text of The Artistic License 2.0, Copyright (c) 2000-2006, The Perl Foundation. GitHub gives the SPDX id Artistic-2.0.

| file of the run | path in the repository | sha256 |
|---|---|---|
| cremona-allcurves-00000-09999.txt | allcurves/allcurves.00000-09999 | 259f3846329395b371e8079c77a6f1097adaebc98a054974573e241416efa968 |
| cremona-aplist-00000-09999.txt | aplist/aplist.00000-09999 | a1cc11fb2c53b58bcf03600cd67d8d9133a14381f1df9dac7b096c20699eca65 |
| cremona-alllabels-00000-09999.txt | alllabels/alllabels.00000-09999 | bc06d9bd10dbba36ddb84ad2fc407d2a71c8c89f22361befae8eda08aa18a377 |
| cremona-readme.txt | README.md | 619466f9a1542c3bfeaa68b592feb903edd205c652cac59d7f21d70444203bb5 |
| cremona-file-format.txt | docs/file-format.txt | 6ed8ed51d79425a53f4fea78004446576fafba81bc2a32c34b954253ade3cb1a |
| cremona-licence.txt | LICENSE | e7000d1562eb8d32209576028f36bf5caed23f01e9a99fa318063cc4684afc01 |

The run checks the sha256 of each file, and it stops when a file does not have the sha256 of the spec. The files are not in the run. The files cover the conductors from 1 to 9999, and the run uses the lines with N <= 1000.

The LMFDB API is not a source of this run. It sent a reCAPTCHA page in place of the second page of curves and of the first page of newforms, so the reads stopped there.

The curve data has 2463 isogeny classes of conductor N <= 1000. The run uses curve number 1 of each class in the Cremona numbering. The a_p are the same for all the curves of a class, because isogenous curves have the same L-series. The aplist has 2463 classes of these conductors.

## What the data says about the aplist

The README does not say how the aplist was computed. It says: "This is a repository of the data files containing the Cremona Database of all elliptic curves over Q of bounded conductor." It also says: "For a description of how most of the data here was computed, see the ANTS 7 Proceedings", and "For a description of the algorithms used, see the book Algorithms for Modular Elliptic Curves". The README does not use the words modular symbols.

The file docs/file-format.txt defines the field of the aplist. It says: "AP: a2 a3 a5 a7 a11 (etc.) where each ap is the p'th eigenvalue of the newform (integers, separated by whitespace). When p divides N this is the W_p eigenvalue, shown just as "+" or "-"; else the T_p eigenvalue." It also says: "AP25: AP for all primes<100 (the first 25 primes)." and that BQ gives "the eigenvalue of W_q and the value of q" for the primes q > 100 of N. The line of the aplist is N CLASSCODE AP25 BQ.

Thus the data calls these numbers eigenvalues of the newform. The book describes the method of modular symbols, but the run does not check that each line of the aplist comes from this method. The run treats the aplist as the newform side only on the word of docs/file-format.txt and of the book.

## What the run does

For each class of conductor N, the run computes a_p = p - #{(x, y) in F_p^2 on the Weierstrass equation} for each prime p of the aplist line: the 25 primes p < 100 and the primes q > 100 of N. For odd p, it completes the square in y and counts the square roots of each value with a table of the squares mod p. For p = 2, it counts all the pairs (x, y).

The models of allcurves are global minimal models. At a good prime the count gives the trace of Frobenius. At a bad prime the count gives 1 for split multiplicative reduction, -1 for nonsplit multiplicative reduction and 0 for additive reduction. The run checks that a_p = 0 exactly when p^2 divides N, and that the primes of the discriminant are the primes of N. It also tests v_p(Delta) < 12, v_p(c4) < 4 or v_p(c6) < 6, which proves that the model is minimal at p. A model that is not minimal at p has v_p(c4) >= 4, so it has a cusp mod p and the count gives 0. Thus a count of 1 or -1 is correct with no test, and the test matters only when p^2 divides N.

For p not dividing N, the aplist gives a_p of the newform, and the run compares it with a_p of the curve. For p dividing N, the aplist gives only the sign w_p of the Atkin-Lehner involution W_p. For a newform of weight 2 and trivial character, a_p = -w_p when p || N, and a_p = 0 when p^2 | N (Atkin and Lehner, 1970). The run uses these two facts to get a_p of the newform at the primes of N. Thus at a prime p with p^2 | N, the value 0 on the newform side comes from the theory, not from the aplist. The arithmetic is exact.

The Sturm bound is B(N) = floor(N prod_{p | N} (1 + 1/p) / 6). A class is Sturm-complete when the aplist has each prime p <= B(N). On both sides the a_n with n <= B(N) come from the a_p with p <= B(N) by the same Hecke relations, so for a Sturm-complete class the a_n of the curve and of the newform agree for all n <= B(N). For the other classes the check is partial: it stops at p = 97, below B(N).

## Counts

| conductors | classes | aplist classes | paired | primes checked | mismatches | Sturm-complete | point of order 2 | Livne set checked | candidates |
|---|---|---|---|---|---|---|---|---|---|
| 1 to 100 | 93 | 93 | 93 | 2325 | 0 | 93 | 55 | 51 | 93 |
| 101 to 200 | 188 | 188 | 188 | 4708 | 0 | 188 | 78 | 56 | 188 |
| 201 to 300 | 194 | 194 | 194 | 4875 | 0 | 179 | 86 | 63 | 179 |
| 301 to 400 | 247 | 247 | 247 | 6210 | 0 | 125 | 102 | 62 | 125 |
| 401 to 500 | 249 | 249 | 249 | 6248 | 0 | 40 | 103 | 51 | 40 |
| 501 to 600 | 274 | 274 | 274 | 6887 | 0 | 18 | 118 | 65 | 18 |
| 601 to 700 | 273 | 273 | 273 | 6876 | 0 | 0 | 110 | 40 | 0 |
| 701 to 800 | 314 | 314 | 314 | 7907 | 0 | 0 | 117 | 62 | 0 |
| 801 to 900 | 305 | 305 | 305 | 7687 | 0 | 0 | 103 | 34 | 0 |
| 901 to 1000 | 326 | 326 | 326 | 8221 | 0 | 0 | 103 | 46 | 0 |
| all | 2463 | 2463 | 2463 | 61944 | 0 | 643 | 975 | 530 | 643 |

A prime checked is a pair of a class and a prime of its aplist line, at which the run compares a_p.

## Mismatches

The run finds no mismatch. At each prime checked, a_p of the curve is equal to a_p of the newform.

## Which N reach the Sturm bound

The data has classes at 707 conductors N <= 1000. At 287 of them the aplist primes reach B(N), and at 420 of them they do not. The aplist has all the primes p < 100 and, above 100, only the primes of N. Thus a class is Sturm-complete exactly when each prime p with 100 < p <= B(N) divides N. This is so when B(N) <= 100, that is when N prod_{p | N} (1 + 1/p) <= 605. It is also so at N = 404 with B(N) = 102 and N = 505 with B(N) = 102, because the primes from 101 to B(N) divide N there.

Each conductor N < 270 of the data is Sturm-complete. No conductor N > 593 is Sturm-complete. From 270 to 593, the Sturm-complete conductors of the data are: 272, 273, 274, 275, 277, 278, 280, 282, 285, 286, 288, 289, 290, 291, 296, 297, 298, 302, 303, 304, 307, 308, 309, 310, 314, 315, 316, 319, 320, 322, 323, 325, 326, 327, 328, 329, 331, 333, 334, 335, 338, 339, 344, 345, 346, 347, 352, 353, 355, 356, 357, 358, 359, 361, 362, 363, 368, 369, 371, 373, 377, 381, 385, 387, 389, 395, 398, 404, 415, 417, 423, 425, 427, 431, 433, 437, 443, 451, 467, 469, 473, 475, 481, 485, 493, 497, 503, 505, 517, 551, 557, 563, 571, 593.

Thus 643 of the 2463 classes are Sturm-complete. For the other 1820 classes the check is partial: the run compares a_p only for p < 100 and the primes of N, and it does not reach B(N).

## Bad primes

The classes have 6434 bad primes in total: 2435 of split multiplicative reduction, 2378 of nonsplit multiplicative reduction and 1621 of additive reduction. At 6434 of them the type agrees with the exponent of p in N. At 6315 of them the test of valuations proves that the model is minimal at p; at the other 119 the count gives 0 in any case, and p^2 divides N. For 2463 of the 2463 classes the primes of the discriminant are the primes of N.

## The criterion of Livne

Livne's criterion (R. Livne, Cubic exponential sums and Galois representations, 1987) compares two continuous representations rho_1 and rho_2 of the Galois group of Q into GL_2(Z_2) that are unramified outside a finite set S of primes. Suppose that the traces of rho_1 and rho_2 are even and that their determinants agree mod 2. Let T be a set of primes outside S whose Frobenius elements in the Galois group of the compositum of the quadratic extensions of Q unramified outside S make a non-cubic set. If the traces and the determinants of rho_1 and rho_2 agree at Frob_p for each p in T, then rho_1 and rho_2 have the same semisimplification.

For a curve E of conductor N and its newform f, S is 2 and the primes of N. Both determinants are the 2-adic cyclotomic character. The Galois group of the compositum is F_2^t, with t = 1 + the number of primes of S. The coordinates of Frob_p are the values of the quadratic characters (d/p) for d = -1, 2 and the odd primes of N, with 1 for the value -1.

A subset T of F_2^t is non-cubic when each cubic form on F_2^t that vanishes on T vanishes on all of F_2^t. On F_2^t the cubic forms are the sums of the monomials x_I with 1 <= |I| <= 3, because x^2 = x. Thus T is non-cubic exactly when the matrix of these monomials at the points of T has full rank. The run takes the primes outside S in increasing order, and it keeps each prime that raises the rank. Thus the largest prime of T is as small as possible.

The traces of rho_E are even exactly when E has a rational point of order 2. The run finds these points exactly, as the integer roots of X^3 + b2 X^2 + 8 b4 X + 16 b6, with X = 4x. For a class with no such point the criterion does not apply, and the run records its Livne set as not applicable. Such a class needs the method of Serre for a residual image of order 3 or 6, with the cubic fields unramified outside S. The run does not have this method.

The criterion also needs even traces for rho_f. The run does not prove this. It only records whether a_p of the newform is even at each prime of the aplist outside S. The aplist has a_p only for p < 100, so the run checks a Livne set on the newform only when all the primes of T are below 100.

975 of the 2463 classes have a rational point of order 2. The Livne set depends only on S. The table gives one row for each S. A class is in the last column when its a_p agree with the aplist on all of T and a_p of the newform is even at each prime of the aplist outside S.

| S | t | cubic monomials | T | largest prime of T | classes | all of T in the aplist | agree on T, newform even |
|---|---|---|---|---|---|---|---|
| 2 | 2 | 3 | 3, 5, 7 | 7 | 10 | 10 | 10 |
| 2, 3 | 3 | 7 | 5, 7, 11, 13, 17, 19, 23 | 23 | 42 | 42 | 42 |
| 2, 5 | 3 | 7 | 3, 7, 11, 13, 17, 29, 31 | 31 | 33 | 33 | 33 |
| 2, 7 | 3 | 7 | 3, 5, 11, 17, 23, 29, 31 | 31 | 28 | 28 | 28 |
| 2, 13 | 3 | 7 | 3, 5, 7, 11, 23, 29, 41 | 41 | 5 | 5 | 5 |
| 2, 17 | 3 | 7 | 3, 5, 7, 13, 19, 41, 47 | 47 | 16 | 16 | 16 |
| 2, 23 | 3 | 7 | 3, 5, 7, 11, 13, 17, 31 | 31 | 4 | 4 | 4 |
| 2, 29 | 3 | 7 | 3, 5, 7, 17, 31, 37, 59 | 59 | 2 | 2 | 2 |
| 2, 31 | 3 | 7 | 3, 5, 7, 13, 17, 19, 23 | 23 | 4 | 4 | 4 |
| 2, 41 | 3 | 7 | 3, 5, 7, 13, 17, 23, 43 | 43 | 6 | 6 | 6 |
| 2, 47 | 3 | 7 | 3, 5, 7, 11, 23, 37, 41 | 41 | 2 | 2 | 2 |
| 2, 53 | 3 | 7 | 3, 5, 7, 11, 13, 23, 41 | 41 | 2 | 2 | 2 |
| 2, 71 | 3 | 7 | 3, 5, 7, 11, 13, 17, 79 | 79 | 1 | 1 | 1 |
| 2, 73 | 3 | 7 | 3, 5, 7, 11, 17, 23, 37 | 37 | 1 | 1 | 1 |
| 2, 79 | 3 | 7 | 3, 5, 7, 11, 17, 23, 29 | 29 | 1 | 1 | 1 |
| 2, 89 | 3 | 7 | 3, 5, 7, 11, 13, 41, 47 | 47 | 3 | 3 | 3 |
| 2, 97 | 3 | 7 | 3, 5, 7, 17, 19, 31, 53 | 53 | 2 | 2 | 2 |
| 2, 103 | 3 | 7 | 3, 5, 7, 13, 19, 31, 73 | 73 | 1 | 1 | 1 |
| 2, 113 | 3 | 7 | 3, 5, 7, 11, 13, 17, 23 | 23 | 3 | 3 | 3 |
| 2, 127 | 3 | 7 | 3, 5, 7, 11, 13, 31, 89 | 89 | 2 | 2 | 2 |
| 2, 137 | 3 | 7 | 3, 5, 7, 11, 23, 37, 41 | 41 | 1 | 1 | 1 |
| 2, 151 | 3 | 7 | 3, 5, 7, 11, 13, 31, 41 | 41 | 1 | 1 | 1 |
| 2, 173 | 3 | 7 | 3, 5, 7, 13, 17, 23, 43 | 43 | 1 | 1 | 1 |
| 2, 199 | 3 | 7 | 3, 5, 7, 17, 37, 43, 71 | 71 | 1 | 1 | 1 |
| 2, 223 | 3 | 7 | 3, 5, 7, 19, 23, 29, 97 | 97 | 1 | 1 | 1 |
| 2, 229 | 3 | 7 | 3, 5, 7, 13, 41, 59, 71 | 71 | 1 | 1 | 1 |
| 2, 233 | 3 | 7 | 3, 5, 7, 13, 17, 19, 47 | 47 | 2 | 2 | 2 |
| 2, 257 | 3 | 7 | 3, 5, 7, 11, 13, 23, 41 | 41 | 2 | 2 | 2 |
| 2, 271 | 3 | 7 | 3, 5, 7, 11, 13, 23, 73 | 73 | 1 | 1 | 1 |
| 2, 281 | 3 | 7 | 3, 5, 7, 13, 23, 41, 43 | 43 | 1 | 1 | 1 |
| 2, 313 | 3 | 7 | 3, 5, 7, 13, 17, 43, 71 | 71 | 1 | 1 | 1 |
| 2, 337 | 3 | 7 | 3, 5, 7, 11, 13, 17, 23 | 23 | 1 | 1 | 1 |
| 2, 353 | 3 | 7 | 3, 5, 7, 11, 23, 29, 89 | 89 | 3 | 3 | 3 |
| 2, 367 | 3 | 7 | 3, 5, 7, 13, 17, 59, 71 | 71 | 1 | 1 | 1 |
| 2, 401 | 3 | 7 | 3, 5, 7, 11, 13, 17, 23 | 23 | 1 | 1 | 1 |
| 2, 431 | 3 | 7 | 3, 5, 7, 13, 17, 23, 43 | 43 | 1 | 1 | 1 |
| 2, 449 | 3 | 7 | 3, 5, 7, 11, 13, 17, 31 | 31 | 1 | 1 | 1 |
| 2, 457 | 3 | 7 | 3, 5, 7, 11, 23, 29, 41 | 41 | 1 | 1 | 1 |
| 2, 463 | 3 | 7 | 3, 5, 7, 29, 31, 41, 43 | 43 | 1 | 1 | 1 |
| 2, 487 | 3 | 7 | 3, 5, 7, 17, 19, 29, 31 | 31 | 1 | 1 | 1 |
| 2, 593 | 3 | 7 | 3, 5, 7, 19, 23, 29, 41 | 41 | 1 | 1 | 1 |
| 2, 3, 5 | 4 | 14 | 7, 11, 13, 17, 19, 23, 29, 31, 41, 43, 53, 61, 71, 73 | 73 | 73 | 73 | 73 |
| 2, 3, 7 | 4 | 14 | 5, 11, 13, 17, 19, 23, 29, 31, 37, 43, 47, 59, 73, 79 | 79 | 47 | 47 | 47 |
| 2, 3, 11 | 4 | 14 | 5, 7, 13, 17, 19, 23, 29, 31, 37, 59, 67, 73, 83, 89 | 89 | 42 | 42 | 42 |
| 2, 3, 13 | 4 | 14 | 5, 7, 11, 17, 19, 23, 29, 37, 41, 43, 47, 61, 73, 79 | 79 | 38 | 38 | 38 |
| 2, 3, 17 | 4 | 14 | 5, 7, 11, 13, 19, 23, 37, 41, 47, 53, 59, 73, 89, 103 | 103 | 17 | 0 | 0 |
| 2, 3, 19 | 4 | 14 | 5, 7, 11, 13, 17, 23, 29, 31, 41, 43, 59, 61, 67, 71 | 71 | 21 | 21 | 21 |
| 2, 3, 23 | 4 | 14 | 5, 7, 11, 13, 17, 19, 29, 31, 37, 41, 47, 59, 97, 139 | 139 | 16 | 0 | 0 |
| 2, 3, 29 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 31, 37, 47, 59, 67, 73, 101 | 101 | 4 | 0 | 0 |
| 2, 3, 31 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 29, 41, 43, 47, 59, 73, 79 | 79 | 3 | 3 | 3 |
| 2, 3, 37 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 31, 41, 47, 53, 59, 67, 97 | 97 | 9 | 9 | 9 |
| 2, 3, 41 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 43, 47, 59, 97 | 97 | 7 | 7 | 7 |
| 2, 3, 43 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 31, 37, 53, 67, 71, 73, 89 | 89 | 9 | 9 | 9 |
| 2, 3, 47 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 31, 37, 41, 53, 59, 71, 73 | 73 | 9 | 9 | 9 |
| 2, 3, 53 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 29, 31, 41, 43, 47, 61, 73 | 73 | 2 | 2 | 2 |
| 2, 3, 59 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 31, 43, 71, 73, 89, 101, 107 | 107 | 4 | 0 | 0 |
| 2, 3, 61 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 29, 37, 41, 43, 47, 83, 103 | 103 | 5 | 0 | 0 |
| 2, 3, 67 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 29, 37, 41, 43, 59, 97, 103 | 103 | 5 | 0 | 0 |
| 2, 3, 71 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 37, 53, 67, 79, 83, 89, 97 | 97 | 3 | 3 | 3 |
| 2, 3, 73 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 37, 41, 43, 47, 79, 149, 193 | 193 | 10 | 0 | 0 |
| 2, 3, 79 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 43, 47, 59, 89 | 89 | 1 | 1 | 1 |
| 2, 3, 83 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 29, 37, 47, 73, 79, 89, 107 | 107 | 4 | 0 | 0 |
| 2, 3, 89 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 29, 41, 47, 59, 67, 79, 109 | 109 | 2 | 0 | 0 |
| 2, 3, 97 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 31, 43, 47, 53, 59, 61, 89 | 89 | 8 | 8 | 8 |
| 2, 3, 101 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 29, 31, 41, 61, 67, 73, 107 | 107 | 1 | 0 | 0 |
| 2, 3, 107 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 29, 41, 43, 59, 71, 73, 79 | 79 | 1 | 1 | 1 |
| 2, 3, 113 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 37, 41, 53, 59, 73, 79, 139 | 139 | 3 | 0 | 0 |
| 2, 3, 131 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 73, 83 | 83 | 2 | 2 | 2 |
| 2, 3, 137 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 31, 37, 41, 43, 83, 97, 101 | 101 | 2 | 0 | 0 |
| 2, 3, 139 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 41, 47, 53, 59, 61, 67, 73 | 73 | 2 | 2 | 2 |
| 2, 3, 163 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 41, 43, 47, 53, 61, 73, 83 | 83 | 1 | 1 | 1 |
| 2, 3, 167 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 29, 43, 47, 59, 61, 73, 79 | 79 | 1 | 1 | 1 |
| 2, 3, 191 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 29, 37, 41, 43, 47, 59, 73 | 73 | 1 | 1 | 1 |
| 2, 3, 193 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 43, 47, 59, 73, 79, 101, 109 | 109 | 1 | 0 | 0 |
| 2, 3, 227 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 29, 31, 67, 83, 89, 109, 191 | 191 | 1 | 0 | 0 |
| 2, 3, 241 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 41, 47, 59, 61, 67, 73, 79 | 79 | 1 | 1 | 1 |
| 2, 3, 313 | 4 | 14 | 5, 7, 11, 13, 17, 19, 23, 29, 37, 43, 59, 71, 73, 79 | 79 | 1 | 1 | 1 |
| 2, 5, 7 | 4 | 14 | 3, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 61, 71 | 71 | 10 | 10 | 10 |
| 2, 5, 11 | 4 | 14 | 3, 7, 13, 17, 19, 23, 29, 31, 37, 41, 43, 59, 79, 97 | 97 | 16 | 16 | 16 |
| 2, 5, 13 | 4 | 14 | 3, 7, 11, 17, 23, 29, 31, 37, 41, 53, 67, 73, 79, 109 | 109 | 12 | 0 | 0 |
| 2, 5, 17 | 4 | 14 | 3, 7, 11, 13, 19, 29, 31, 37, 41, 43, 47, 73, 101, 137 | 137 | 11 | 0 | 0 |
| 2, 5, 19 | 4 | 14 | 3, 7, 11, 13, 17, 29, 31, 41, 43, 59, 61, 97, 103, 157 | 157 | 8 | 0 | 0 |
| 2, 5, 29 | 4 | 14 | 3, 7, 11, 13, 17, 31, 37, 41, 47, 59, 61, 67, 71, 109 | 109 | 5 | 0 | 0 |
| 2, 5, 31 | 4 | 14 | 3, 7, 11, 13, 17, 19, 23, 29, 67, 71, 79, 89, 97, 101 | 101 | 5 | 0 | 0 |
| 2, 5, 37 | 4 | 14 | 3, 7, 11, 13, 17, 19, 23, 29, 31, 43, 53, 71, 73, 89 | 89 | 4 | 4 | 4 |
| 2, 5, 41 | 4 | 14 | 3, 7, 11, 13, 17, 23, 29, 31, 37, 43, 59, 61, 71, 73 | 73 | 7 | 7 | 7 |
| 2, 5, 53 | 4 | 14 | 3, 7, 11, 13, 17, 19, 23, 29, 31, 41, 43, 61, 73, 157 | 157 | 2 | 0 | 0 |
| 2, 5, 59 | 4 | 14 | 3, 7, 11, 13, 17, 19, 23, 29, 31, 43, 53, 61, 71, 73 | 73 | 1 | 1 | 1 |
| 2, 5, 61 | 4 | 14 | 3, 7, 11, 13, 17, 19, 29, 31, 37, 43, 47, 73, 89, 109 | 109 | 2 | 0 | 0 |
| 2, 5, 73 | 4 | 14 | 3, 7, 11, 13, 17, 19, 23, 29, 31, 37, 43, 61, 71, 97 | 97 | 2 | 2 | 2 |
| 2, 5, 79 | 4 | 14 | 3, 7, 11, 13, 17, 23, 29, 31, 37, 41, 59, 67, 71, 73 | 73 | 3 | 3 | 3 |
| 2, 5, 89 | 4 | 14 | 3, 7, 11, 13, 17, 19, 29, 31, 41, 47, 53, 67, 71, 109 | 109 | 5 | 0 | 0 |
| 2, 5, 101 | 4 | 14 | 3, 7, 11, 13, 17, 19, 23, 29, 31, 41, 43, 53, 73, 151 | 151 | 1 | 0 | 0 |
| 2, 5, 109 | 4 | 14 | 3, 7, 11, 13, 17, 23, 29, 31, 41, 67, 73, 79, 101, 131 | 131 | 1 | 0 | 0 |
| 2, 5, 151 | 4 | 14 | 3, 7, 11, 13, 17, 29, 31, 37, 41, 43, 47, 61, 71, 73 | 73 | 1 | 1 | 1 |
| 2, 5, 181 | 4 | 14 | 3, 7, 11, 13, 17, 19, 29, 31, 41, 53, 61, 73, 79, 83 | 83 | 1 | 1 | 1 |
| 2, 5, 191 | 4 | 14 | 3, 7, 11, 13, 17, 23, 29, 31, 37, 41, 59, 73, 79, 83 | 83 | 1 | 1 | 1 |
| 2, 5, 193 | 4 | 14 | 3, 7, 11, 13, 17, 29, 31, 41, 47, 59, 71, 97, 101, 157 | 157 | 1 | 0 | 0 |
| 2, 5, 199 | 4 | 14 | 3, 7, 11, 13, 17, 29, 31, 37, 41, 43, 71, 101, 127, 131 | 131 | 1 | 0 | 0 |
| 2, 7, 11 | 4 | 14 | 3, 5, 13, 17, 19, 23, 29, 31, 37, 43, 67, 79, 89, 167 | 167 | 10 | 0 | 0 |
| 2, 7, 13 | 4 | 14 | 3, 5, 11, 17, 19, 23, 29, 31, 37, 41, 43, 61, 71, 103 | 103 | 1 | 0 | 0 |
| 2, 7, 17 | 4 | 14 | 3, 5, 11, 13, 19, 23, 29, 31, 41, 43, 47, 53, 89, 113 | 113 | 6 | 0 | 0 |
| 2, 7, 19 | 4 | 14 | 3, 5, 11, 13, 17, 23, 29, 31, 41, 47, 67, 71, 83, 113 | 113 | 1 | 0 | 0 |
| 2, 7, 23 | 4 | 14 | 3, 5, 11, 13, 17, 19, 29, 31, 37, 41, 71, 79, 103, 113 | 113 | 5 | 0 | 0 |
| 2, 7, 29 | 4 | 14 | 3, 5, 11, 17, 23, 31, 37, 53, 59, 61, 67, 79, 103, 113 | 113 | 3 | 0 | 0 |
| 2, 7, 31 | 4 | 14 | 3, 5, 11, 13, 17, 19, 23, 29, 41, 47, 67, 71, 109, 137 | 137 | 3 | 0 | 0 |
| 2, 7, 37 | 4 | 14 | 3, 5, 11, 17, 19, 23, 29, 31, 41, 43, 47, 53, 71, 101 | 101 | 1 | 0 | 0 |
| 2, 7, 41 | 4 | 14 | 3, 5, 11, 13, 17, 23, 29, 31, 37, 43, 47, 59, 71, 73 | 73 | 4 | 4 | 4 |
| 2, 7, 43 | 4 | 14 | 3, 5, 11, 13, 17, 23, 29, 31, 53, 59, 71, 73, 113, 163 | 163 | 1 | 0 | 0 |
| 2, 7, 47 | 4 | 14 | 3, 5, 11, 17, 19, 23, 29, 31, 37, 41, 61, 71, 103, 113 | 113 | 2 | 0 | 0 |
| 2, 7, 53 | 4 | 14 | 3, 5, 11, 13, 17, 23, 29, 31, 41, 47, 59, 67, 109, 137 | 137 | 2 | 0 | 0 |
| 2, 7, 67 | 4 | 14 | 3, 5, 11, 17, 19, 23, 29, 31, 41, 47, 53, 79, 107, 113 | 113 | 1 | 0 | 0 |
| 2, 7, 71 | 4 | 14 | 3, 5, 11, 13, 17, 23, 29, 31, 43, 53, 59, 73, 79, 103 | 103 | 5 | 0 | 0 |
| 2, 7, 113 | 4 | 14 | 3, 5, 11, 13, 17, 23, 29, 31, 41, 43, 47, 53, 83, 127 | 127 | 3 | 0 | 0 |
| 2, 11, 17 | 4 | 14 | 3, 5, 7, 13, 19, 23, 29, 41, 47, 53, 59, 97, 107, 127 | 127 | 1 | 0 | 0 |
| 2, 11, 19 | 4 | 14 | 3, 5, 7, 13, 17, 23, 31, 37, 41, 43, 61, 79, 89, 107 | 107 | 2 | 0 | 0 |
| 2, 11, 43 | 4 | 14 | 3, 5, 7, 13, 17, 19, 23, 29, 53, 59, 71, 73, 79, 83 | 83 | 1 | 1 | 1 |
| 2, 11, 79 | 4 | 14 | 3, 5, 7, 13, 17, 19, 23, 29, 37, 43, 47, 67, 73, 113 | 113 | 1 | 0 | 0 |
| 2, 11, 89 | 4 | 14 | 3, 5, 7, 13, 17, 19, 23, 37, 41, 47, 67, 79, 107, 109 | 109 | 1 | 0 | 0 |
| 2, 13, 17 | 4 | 14 | 3, 5, 7, 11, 19, 23, 29, 41, 43, 47, 53, 89, 103, 113 | 113 | 7 | 0 | 0 |
| 2, 13, 19 | 4 | 14 | 3, 5, 7, 11, 23, 29, 31, 37, 41, 43, 59, 61, 73, 79 | 79 | 1 | 1 | 1 |
| 2, 13, 23 | 4 | 14 | 3, 5, 7, 11, 17, 29, 31, 41, 43, 53, 59, 79, 89, 127 | 127 | 1 | 0 | 0 |
| 2, 13, 29 | 4 | 14 | 3, 5, 7, 11, 17, 23, 31, 37, 41, 53, 59, 61, 79, 107 | 107 | 2 | 0 | 0 |
| 2, 13, 37 | 4 | 14 | 3, 5, 7, 11, 17, 19, 23, 29, 31, 41, 43, 53, 89, 127 | 127 | 2 | 0 | 0 |
| 2, 13, 53 | 4 | 14 | 3, 5, 7, 11, 19, 23, 29, 31, 37, 41, 43, 61, 89, 199 | 199 | 1 | 0 | 0 |
| 2, 13, 61 | 4 | 14 | 3, 5, 7, 11, 17, 19, 23, 29, 37, 41, 43, 47, 89, 103 | 103 | 1 | 0 | 0 |
| 2, 17, 19 | 4 | 14 | 3, 5, 7, 11, 13, 29, 31, 41, 43, 47, 59, 73, 89, 101 | 101 | 5 | 0 | 0 |
| 2, 17, 23 | 4 | 14 | 3, 5, 7, 11, 13, 19, 29, 31, 41, 47, 53, 59, 89, 97 | 97 | 3 | 3 | 3 |
| 2, 17, 29 | 4 | 14 | 3, 5, 7, 13, 19, 31, 37, 41, 47, 59, 89, 101, 103, 107 | 107 | 1 | 0 | 0 |
| 2, 17, 47 | 4 | 14 | 3, 5, 7, 11, 13, 19, 23, 37, 41, 53, 59, 97, 103, 127 | 127 | 2 | 0 | 0 |
| 2, 17, 53 | 4 | 14 | 3, 5, 7, 11, 13, 19, 23, 29, 41, 43, 47, 97, 101, 103 | 103 | 2 | 0 | 0 |
| 2, 23, 41 | 4 | 14 | 3, 5, 7, 11, 13, 17, 31, 43, 47, 53, 59, 103, 113, 173 | 173 | 1 | 0 | 0 |
| 2, 3, 5, 7 | 5 | 25 | 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 71, 73, 79, 83, 101, 103, 107, 109, 113, 173, 193 | 193 | 37 | 0 | 0 |
| 2, 3, 5, 11 | 5 | 25 | 7, 13, 17, 19, 23, 29, 31, 37, 41, 43, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97, 103, 113, 131, 167, 239 | 239 | 20 | 0 | 0 |
| 2, 3, 5, 13 | 5 | 25 | 7, 11, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 61, 67, 71, 73, 79, 83, 103, 107, 109, 131, 137, 139, 157 | 157 | 16 | 0 | 0 |
| 2, 3, 5, 17 | 5 | 25 | 7, 11, 13, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 71, 73, 83, 89, 101, 103, 107, 113, 137, 139, 151 | 151 | 10 | 0 | 0 |
| 2, 3, 5, 19 | 5 | 25 | 7, 11, 13, 17, 23, 29, 31, 41, 43, 53, 59, 61, 67, 71, 73, 83, 97, 101, 103, 107, 109, 113, 139, 157, 167 | 167 | 19 | 0 | 0 |
| 2, 3, 5, 23 | 5 | 25 | 7, 11, 13, 17, 19, 29, 31, 37, 41, 43, 47, 53, 59, 61, 71, 73, 79, 83, 89, 97, 127, 139, 149, 163, 241 | 241 | 13 | 0 | 0 |
| 2, 3, 5, 29 | 5 | 25 | 7, 11, 13, 17, 19, 23, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 83, 101, 109, 127, 139, 149, 151, 191 | 191 | 11 | 0 | 0 |
| 2, 3, 5, 31 | 5 | 25 | 7, 11, 13, 17, 19, 23, 29, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97, 101, 107, 109, 113, 127 | 127 | 12 | 0 | 0 |
| 2, 3, 5, 41 | 5 | 25 | 7, 11, 13, 17, 19, 23, 29, 31, 37, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97, 103, 109, 113, 139 | 139 | 1 | 0 | 0 |
| 2, 3, 5, 43 | 5 | 25 | 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 53, 61, 67, 71, 73, 83, 89, 97, 101, 103, 109, 113, 131, 139, 151 | 151 | 2 | 0 | 0 |
| 2, 3, 5, 47 | 5 | 25 | 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 53, 59, 61, 71, 73, 79, 83, 89, 97, 101, 107, 109, 113, 263 | 263 | 1 | 0 | 0 |
| 2, 3, 5, 53 | 5 | 25 | 7, 11, 13, 17, 19, 23, 29, 31, 41, 43, 47, 61, 67, 71, 73, 83, 89, 97, 101, 103, 107, 137, 157, 173, 179 | 179 | 2 | 0 | 0 |
| 2, 3, 5, 59 | 5 | 25 | 7, 11, 13, 17, 19, 23, 29, 31, 41, 43, 53, 61, 71, 73, 79, 83, 89, 101, 103, 107, 113, 163, 167, 173, 181 | 181 | 1 | 0 | 0 |
| 2, 3, 5, 61 | 5 | 25 | 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 71, 73, 83, 89, 103, 109, 113, 131, 139, 149, 163, 197 | 197 | 2 | 0 | 0 |
| 2, 3, 7, 11 | 5 | 25 | 5, 13, 17, 19, 23, 29, 31, 37, 43, 47, 53, 59, 67, 73, 79, 83, 89, 97, 101, 107, 109, 113, 157, 167, 179 | 179 | 10 | 0 | 0 |
| 2, 3, 7, 13 | 5 | 25 | 5, 11, 17, 19, 23, 29, 31, 37, 41, 43, 47, 59, 61, 67, 71, 73, 79, 101, 103, 107, 113, 131, 137, 139, 193 | 193 | 4 | 0 | 0 |
| 2, 3, 7, 17 | 5 | 25 | 5, 11, 13, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 73, 79, 89, 101, 103, 113, 127, 131, 137, 139, 167 | 167 | 4 | 0 | 0 |
| 2, 3, 7, 19 | 5 | 25 | 5, 11, 13, 17, 23, 29, 31, 37, 41, 43, 47, 59, 61, 67, 71, 73, 79, 83, 97, 107, 113, 137, 139, 167, 193 | 193 | 12 | 0 | 0 |
| 2, 3, 7, 23 | 5 | 25 | 5, 11, 13, 17, 19, 29, 31, 37, 41, 43, 47, 53, 59, 61, 71, 73, 79, 83, 97, 101, 103, 113, 127, 139, 179 | 179 | 7 | 0 | 0 |
| 2, 3, 7, 29 | 5 | 25 | 5, 11, 13, 17, 19, 23, 31, 37, 43, 47, 53, 59, 61, 67, 73, 79, 101, 103, 107, 109, 113, 131, 139, 151, 167 | 167 | 2 | 0 | 0 |
| 2, 3, 7, 31 | 5 | 25 | 5, 11, 13, 17, 19, 23, 29, 37, 41, 43, 47, 59, 67, 71, 73, 79, 83, 97, 103, 107, 109, 113, 137, 139, 149 | 149 | 4 | 0 | 0 |
| 2, 3, 7, 37 | 5 | 25 | 5, 11, 13, 17, 19, 23, 29, 31, 41, 43, 47, 53, 59, 67, 71, 73, 79, 83, 97, 101, 109, 113, 127, 137, 139 | 139 | 3 | 0 | 0 |
| 2, 3, 7, 41 | 5 | 25 | 5, 11, 13, 17, 19, 23, 29, 31, 37, 43, 47, 59, 61, 67, 71, 73, 79, 97, 101, 107, 109, 113, 127, 137, 139 | 139 | 1 | 0 | 0 |
| 2, 3, 7, 47 | 5 | 25 | 5, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 53, 59, 61, 71, 73, 79, 97, 101, 103, 109, 113, 127, 167, 193 | 193 | 3 | 0 | 0 |
| 2, 3, 11, 13 | 5 | 25 | 5, 7, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 73, 79, 83, 89, 97, 103, 107, 109, 113, 157 | 157 | 10 | 0 | 0 |
| 2, 3, 11, 17 | 5 | 25 | 5, 7, 13, 19, 23, 29, 31, 37, 41, 47, 53, 59, 61, 67, 73, 83, 89, 97, 101, 103, 107, 113, 127, 157, 163 | 163 | 1 | 0 | 0 |
| 2, 3, 11, 23 | 5 | 25 | 5, 7, 13, 17, 19, 29, 31, 37, 41, 47, 59, 61, 67, 73, 83, 89, 97, 103, 127, 131, 139, 149, 163, 167, 191 | 191 | 2 | 0 | 0 |
| 2, 3, 11, 29 | 5 | 25 | 5, 7, 13, 17, 19, 23, 31, 37, 47, 59, 61, 67, 73, 79, 83, 89, 97, 101, 103, 131, 139, 149, 163, 167, 181 | 181 | 1 | 0 | 0 |
| 2, 3, 13, 17 | 5 | 25 | 5, 7, 11, 19, 23, 29, 37, 41, 43, 47, 53, 59, 61, 71, 73, 79, 89, 103, 107, 113, 139, 149, 151, 157, 179 | 179 | 3 | 0 | 0 |
| 2, 3, 13, 23 | 5 | 25 | 5, 7, 11, 17, 19, 29, 31, 37, 41, 43, 47, 53, 59, 61, 73, 79, 89, 97, 107, 127, 131, 139, 163, 191, 197 | 197 | 6 | 0 | 0 |
| 2, 3, 17, 19 | 5 | 25 | 5, 7, 11, 13, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 83, 89, 97, 101, 103, 107, 137, 157 | 157 | 1 | 0 | 0 |
| 2, 5, 7, 11 | 5 | 25 | 3, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 59, 61, 67, 71, 79, 83, 89, 97, 113, 127, 157, 167, 179, 181 | 181 | 9 | 0 | 0 |
| 2, 5, 7, 13 | 5 | 25 | 3, 11, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 61, 67, 71, 73, 79, 83, 103, 109, 113, 131, 137, 179, 199 | 199 | 9 | 0 | 0 |
| 2, 5, 7, 19 | 5 | 25 | 3, 11, 13, 17, 23, 29, 31, 37, 41, 43, 47, 59, 61, 67, 71, 83, 97, 103, 113, 127, 131, 137, 149, 157, 179 | 179 | 1 | 0 | 0 |
| 2, 5, 7, 23 | 5 | 25 | 3, 11, 13, 17, 19, 29, 31, 37, 41, 43, 47, 59, 61, 71, 73, 79, 83, 89, 101, 103, 109, 113, 127, 157, 179 | 179 | 2 | 0 | 0 |

## Candidates for certificates

Spec 13.4 gives two certificates. The Sturm bound makes the equality of two modular forms of weight 2 on Gamma0(N) a finite check of the coefficients a_n with n <= B(N). It does not show that the L-series of E is a modular form. Thus the Sturm bound alone does not certify the modularity of E. The theorem of Faltings-Serre-Livne, as a named hypothesis, makes the equality of rho_E and rho_f a finite check of a_p on T.

A Sturm-complete candidate is a class that agrees with the aplist at all its primes and whose aplist primes reach B(N). Only these classes are Sturm-complete candidates. A certificate for such a class also needs items that the run does not give: a check in Lean that the newform exists with these a_p, for example against a basis of the cusp forms of level N, and a proof of the modularity of E or the criterion of Livne.

Sturm-complete candidates (643), with their LMFDB labels: 11.a, 14.a, 15.a, 17.a, 19.a, 20.a, 21.a, 24.a, 26.a, 26.b, 27.a, 30.a, 32.a, 33.a, 34.a, 35.a, 36.a, 37.a, 37.b, 38.a, 38.b, 39.a, 40.a, 42.a, 43.a, 44.a, 45.a, 46.a, 48.a, 49.a, 50.a, 50.b, 51.a, 52.a, 53.a, 54.a, 54.b, 55.a, 56.a, 56.b, 57.a, 57.c, 57.b, 58.a, 58.b, 61.a, 62.a, 63.a, 64.a, 65.a, 66.a, 66.b, 66.c, 67.a, 69.a, 70.a, 72.a, 73.a, 75.c, 75.b, 75.a, 76.a, 77.a, 77.b, 77.c, 78.a, 79.a, 80.a, 80.b, 82.a, 83.a, 84.b, 84.a, 85.a, 88.a, 89.a, 89.b, 90.a, 90.b, 90.c, 91.a, 91.b, 92.b, 92.a, 94.a, 96.b, 96.a, 98.a, 99.a, 99.b, 99.c, 99.d, 100.a, 101.a, 102.a, 102.c, 102.b, 104.a, 105.a, 106.c, 106.a, 106.d, 106.b, 108.a, 109.a, 110.b, 110.c, 110.a, 112.a, 112.b, 112.c, 113.a, 114.c, 114.a, 114.b, 115.a, 116.a, 116.b, 116.c, 117.a, 118.a, 118.c, 118.d, 118.b, 120.b, 120.a, 121.a, 121.b, 121.c, 121.d, 122.a, 123.a, 123.b, 124.a, 124.b, 126.b, 126.a, 128.a, 128.b, 128.c, 128.d, 129.a, 129.b, 130.a, 130.b, 130.c, 131.a, 132.b, 132.a, 135.a, 135.b, 136.a, 136.b, 138.a, 138.b, 138.c, 139.a, 140.a, 140.b, 141.a, 141.b, 141.c, 141.d, 141.e, 142.d, 142.a, 142.b, 142.e, 142.c, 143.a, 144.a, 144.b, 145.a, 147.a, 147.c, 147.b, 148.a, 150.c, 150.a, 150.b, 152.a, 152.b, 153.a, 153.b, 153.c, 153.d, 154.a, 154.c, 154.b, 155.a, 155.b, 155.c, 156.a, 156.b, 158.c, 158.a, 158.d, 158.b, 158.e, 160.a, 160.b, 161.a, 162.a, 162.c, 162.b, 162.d, 163.a, 166.a, 168.b, 168.a, 170.b, 170.a, 170.e, 170.c, 170.d, 171.a, 171.b, 171.c, 171.d, 172.a, 174.b, 174.e, 174.d, 174.c, 174.a, 175.a, 175.b, 175.c, 176.c, 176.b, 176.a, 178.b, 178.a, 179.a, 180.a, 182.c, 182.d, 182.a, 182.e, 182.b, 184.a, 184.b, 184.c, 184.d, 185.a, 185.b, 185.c, 186.a, 186.c, 186.b, 187.a, 187.b, 189.a, 189.b, 189.c, 189.d, 190.b, 190.a, 190.c, 192.a, 192.c, 192.d, 192.b, 194.a, 195.a, 195.d, 195.c, 195.b, 196.a, 196.b, 197.a, 198.a, 198.e, 198.d, 198.b, 198.c, 200.a, 200.b, 200.c, 200.d, 200.e, 201.a, 201.b, 201.c, 202.a, 203.a, 203.b, 203.c, 204.a, 204.b, 205.a, 205.b, 205.c, 206.a, 207.a, 208.a, 208.b, 208.c, 208.d, 209.a, 210.d, 210.b, 210.c, 210.a, 210.e, 212.a, 212.b, 213.a, 214.c, 214.a, 214.b, 214.d, 215.a, 216.a, 216.b, 216.c, 216.d, 218.a, 219.a, 219.b, 219.c, 220.a, 220.b, 221.a, 221.b, 222.e, 222.d, 222.b, 222.c, 222.a, 224.a, 224.b, 225.c, 225.d, 225.b, 225.e, 225.a, 226.a, 228.b, 228.a, 229.a, 231.a, 232.a, 232.b, 233.a, 234.b, 234.d, 234.a, 234.c, 234.e, 235.b, 235.a, 235.c, 236.a, 236.b, 238.c, 238.a, 238.d, 238.e, 238.b, 240.c, 240.b, 240.a, 240.d, 242.b, 242.a, 243.a, 243.b, 244.a, 245.a, 245.b, 245.c, 246.e, 246.g, 246.c, 246.a, 246.f, 246.d, 246.b, 248.a, 248.b, 248.c, 249.a, 249.b, 252.b, 252.a, 254.b, 254.c, 254.a, 254.d, 256.a, 256.b, 256.c, 256.d, 258.b, 258.a, 258.c, 258.d, 258.e, 258.f, 258.g, 259.a, 260.a, 262.b, 262.a, 264.c, 264.a, 264.b, 264.d, 265.a, 267.b, 267.a, 268.a, 269.a, 272.a, 272.b, 272.c, 272.d, 273.a, 273.b, 274.c, 274.a, 274.b, 275.a, 275.b, 277.a, 278.b, 278.a, 280.b, 280.a, 282.b, 282.a, 285.a, 285.b, 285.c, 286.a, 286.c, 286.b, 286.d, 286.e, 286.f, 288.a, 288.b, 288.c, 288.d, 288.e, 289.a, 290.a, 291.a, 291.b, 291.c, 291.d, 296.a, 296.b, 297.a, 297.b, 297.c, 297.d, 298.b, 298.a, 302.c, 302.a, 302.b, 303.b, 303.a, 304.d, 304.c, 304.b, 304.e, 304.f, 304.a, 307.a, 307.b, 307.c, 307.d, 308.a, 309.a, 310.b, 310.a, 314.a, 315.b, 315.a, 316.b, 316.a, 319.a, 320.d, 320.c, 320.f, 320.e, 320.b, 320.a, 322.a, 322.b, 322.d, 322.c, 323.a, 325.c, 325.b, 325.d, 325.e, 325.a, 326.b, 326.c, 326.a, 327.a, 328.a, 328.b, 329.a, 331.a, 333.b, 333.c, 333.a, 333.d, 334.a, 335.a, 338.c, 338.e, 338.f, 338.b, 338.d, 338.a, 339.b, 339.c, 339.a, 344.a, 345.c, 345.d, 345.e, 345.b, 345.f, 345.a, 346.b, 346.a, 347.a, 352.e, 352.d, 352.c, 352.b, 352.f, 352.a, 353.a, 355.a, 356.a, 357.b, 357.c, 357.d, 357.a, 358.a, 358.b, 359.b, 359.a, 361.a, 361.b, 362.a, 362.b, 363.b, 363.c, 363.a, 368.c, 368.d, 368.f, 368.e, 368.b, 368.g, 368.a, 369.a, 369.b, 371.a, 371.b, 373.a, 377.a, 381.a, 381.b, 385.b, 385.a, 387.c, 387.d, 387.b, 387.a, 387.e, 389.a, 395.b, 395.c, 395.a, 398.a, 404.b, 404.a, 415.a, 417.a, 423.c, 423.e, 423.d, 423.g, 423.f, 423.b, 423.a, 425.d, 425.c, 425.b, 425.a, 427.b, 427.c, 427.a, 431.a, 431.b, 433.a, 437.a, 437.b, 443.b, 443.a, 443.c, 451.a, 467.a, 469.b, 469.a, 473.a, 475.b, 475.c, 475.a, 481.a, 485.a, 485.b, 493.b, 493.a, 497.a, 503.b, 503.c, 503.a, 505.a, 517.c, 517.a, 517.b, 551.c, 551.b, 551.d, 551.a, 557.a, 557.b, 563.a, 571.b, 571.a, 593.b, 593.a.

The classes that agree on all of their Livne set, with a_p of the newform even at each prime of the aplist outside S (530): 14.a, 15.a, 17.a, 20.a, 21.a, 24.a, 30.a, 32.a, 33.a, 34.a, 36.a, 39.a, 40.a, 42.a, 45.a, 46.a, 48.a, 49.a, 52.a, 55.a, 56.a, 56.b, 57.c, 62.a, 63.a, 64.a, 66.a, 66.b, 66.c, 70.a, 72.a, 73.a, 75.b, 78.a, 80.a, 80.b, 82.a, 84.b, 84.a, 89.b, 90.a, 90.b, 90.c, 94.a, 96.b, 96.a, 98.a, 99.a, 99.b, 99.c, 100.a, 112.a, 112.b, 112.c, 113.a, 114.c, 114.a, 114.b, 116.c, 117.a, 120.b, 120.a, 126.b, 126.a, 128.a, 128.b, 128.c, 128.d, 129.b, 132.b, 132.a, 136.a, 136.b, 141.b, 141.c, 142.b, 144.a, 144.b, 147.a, 150.c, 150.a, 150.b, 156.a, 156.b, 158.e, 160.a, 160.b, 168.b, 168.a, 171.a, 178.a, 180.a, 184.c, 185.c, 192.a, 192.c, 192.d, 192.b, 194.a, 198.a, 198.e, 198.d, 198.b, 198.c, 200.b, 200.c, 200.d, 205.a, 205.b, 205.c, 206.a, 208.c, 212.b, 213.a, 220.a, 220.b, 222.b, 224.a, 224.b, 225.b, 226.a, 228.b, 233.a, 234.d, 234.a, 234.c, 240.c, 240.b, 240.a, 240.d, 246.c, 246.a, 246.f, 248.b, 252.b, 252.a, 254.c, 254.d, 256.a, 256.b, 256.c, 256.d, 258.a, 258.d, 258.g, 264.c, 264.a, 264.b, 264.d, 272.a, 272.b, 272.c, 272.d, 274.b, 275.a, 282.b, 282.a, 288.a, 288.b, 288.c, 288.d, 288.e, 289.a, 291.b, 291.c, 294.g, 294.b, 294.c, 300.d, 300.a, 302.a, 312.e, 312.b, 312.f, 312.a, 312.c, 312.d, 320.d, 320.c, 320.f, 320.e, 320.b, 320.a, 328.a, 328.b, 333.c, 333.a, 336.b, 336.c, 336.e, 336.d, 336.a, 336.f, 342.f, 342.c, 342.g, 342.a, 342.b, 350.b, 350.f, 353.a, 360.b, 360.c, 360.d, 360.e, 360.a, 363.b, 368.c, 368.d, 370.b, 370.d, 372.c, 384.g, 384.c, 384.f, 384.b, 384.h, 384.d, 384.a, 384.e, 387.a, 392.d, 392.b, 395.b, 395.c, 396.b, 396.a, 398.a, 400.e, 400.g, 400.c, 400.b, 410.b, 410.d, 410.a, 410.c, 423.e, 423.d, 426.a, 440.a, 440.b, 440.c, 441.f, 441.c, 444.a, 444.b, 446.d, 448.d, 448.e, 448.g, 448.f, 448.h, 448.a, 448.b, 448.c, 450.f, 450.b, 450.e, 450.a, 450.d, 456.b, 456.d, 464.a, 466.a, 468.e, 468.a, 468.b, 468.c, 468.d, 480.b, 480.d, 480.e, 480.f, 480.a, 480.c, 480.g, 480.h, 490.f, 490.h, 490.i, 494.b, 496.f, 496.b, 501.a, 504.a, 504.g, 504.c, 504.f, 504.d, 504.b, 504.e, 504.h, 507.a, 514.b, 514.a, 516.c, 528.c, 528.b, 528.f, 528.i, 528.e, 528.a, 528.d, 528.g, 528.h, 528.j, 542.b, 544.c, 544.e, 544.a, 544.d, 544.f, 544.b, 550.c, 550.k, 558.c, 560.d, 562.a, 573.b, 574.d, 574.e, 574.a, 574.j, 576.e, 576.h, 576.g, 576.d, 576.f, 576.i, 576.a, 576.c, 576.b, 578.a, 582.a, 582.c, 582.b, 582.d, 588.c, 588.b, 588.e, 588.d, 590.c, 593.a, 600.c, 600.d, 600.h, 600.a, 600.g, 605.b, 624.c, 624.a, 624.d, 624.g, 624.j, 624.f, 624.b, 624.i, 624.h, 624.e, 626.a, 639.a, 640.d, 640.c, 640.f, 640.h, 640.g, 640.a, 640.e, 640.b, 642.a, 656.b, 656.a, 656.c, 666.f, 672.c, 672.e, 672.d, 672.a, 672.b, 672.f, 672.g, 672.h, 674.c, 676.c, 684.a, 692.a, 700.f, 700.h, 706.c, 706.b, 712.a, 720.a, 720.i, 720.d, 720.e, 720.f, 720.b, 720.g, 720.c, 720.h, 720.j, 723.a, 726.b, 726.c, 726.d, 726.g, 726.i, 730.d, 730.e, 734.a, 738.d, 738.j, 738.i, 738.h, 744.f, 752.a, 755.b, 768.b, 768.a, 768.g, 768.h, 768.c, 768.d, 768.f, 768.e, 774.d, 774.b, 774.h, 776.a, 782.a, 782.b, 782.c, 784.e, 784.i, 784.f, 784.b, 786.d, 786.k, 790.a, 792.c, 792.e, 792.d, 792.b, 792.f, 792.a, 800.d, 800.a, 800.f, 800.i, 800.e, 802.a, 832.e, 832.f, 834.b, 834.f, 846.c, 846.b, 846.a, 848.b, 862.e, 873.b, 873.c, 880.e, 880.f, 880.g, 880.b, 880.h, 880.j, 882.b, 882.i, 882.l, 882.f, 888.c, 888.b, 888.d, 896.b, 896.a, 896.d, 896.c, 898.d, 900.g, 900.b, 900.h, 900.a, 904.a, 905.b, 912.e, 912.l, 912.c, 912.b, 912.h, 912.j, 912.k, 914.a, 916.c, 925.a, 926.a, 936.c, 936.i, 936.a, 936.b, 936.g, 936.e, 936.d, 936.h, 939.c, 946.a, 948.a, 954.b, 954.l, 955.a, 960.b, 960.c, 960.g, 960.h, 960.e, 960.k, 960.l, 960.m, 960.a, 960.d, 960.f, 960.j, 960.i, 960.o, 960.p, 960.n, 974.c, 978.d, 980.h.

The classes in both lists (187): 14.a, 15.a, 17.a, 20.a, 21.a, 24.a, 30.a, 32.a, 33.a, 34.a, 36.a, 39.a, 40.a, 42.a, 45.a, 46.a, 48.a, 49.a, 52.a, 55.a, 56.a, 56.b, 57.c, 62.a, 63.a, 64.a, 66.a, 66.b, 66.c, 70.a, 72.a, 73.a, 75.b, 78.a, 80.a, 80.b, 82.a, 84.b, 84.a, 89.b, 90.a, 90.b, 90.c, 94.a, 96.b, 96.a, 98.a, 99.a, 99.b, 99.c, 100.a, 112.a, 112.b, 112.c, 113.a, 114.c, 114.a, 114.b, 116.c, 117.a, 120.b, 120.a, 126.b, 126.a, 128.a, 128.b, 128.c, 128.d, 129.b, 132.b, 132.a, 136.a, 136.b, 141.b, 141.c, 142.b, 144.a, 144.b, 147.a, 150.c, 150.a, 150.b, 156.a, 156.b, 158.e, 160.a, 160.b, 168.b, 168.a, 171.a, 178.a, 180.a, 184.c, 185.c, 192.a, 192.c, 192.d, 192.b, 194.a, 198.a, 198.e, 198.d, 198.b, 198.c, 200.b, 200.c, 200.d, 205.a, 205.b, 205.c, 206.a, 208.c, 212.b, 213.a, 220.a, 220.b, 222.b, 224.a, 224.b, 225.b, 226.a, 228.b, 233.a, 234.d, 234.a, 234.c, 240.c, 240.b, 240.a, 240.d, 246.c, 246.a, 246.f, 248.b, 252.b, 252.a, 254.c, 254.d, 256.a, 256.b, 256.c, 256.d, 258.a, 258.d, 258.g, 264.c, 264.a, 264.b, 264.d, 272.a, 272.b, 272.c, 272.d, 274.b, 275.a, 282.b, 282.a, 288.a, 288.b, 288.c, 288.d, 288.e, 289.a, 291.b, 291.c, 302.a, 320.d, 320.c, 320.f, 320.e, 320.b, 320.a, 328.a, 328.b, 333.c, 333.a, 353.a, 363.b, 368.c, 368.d, 387.a, 395.b, 395.c, 398.a, 423.e, 423.d, 593.a. For these classes the run gives both finite checks of spec 13.4, with the two hypotheses above still open.

The other 1820 classes agree with the aplist, but the check is partial: their aplist primes do not reach B(N). classes.json gives the primes below B(N) that the aplist does not have.

## Sources

- J. E. Cremona, Algorithms for modular elliptic curves, second edition, 1997: the method of the data.
- J. E. Cremona, the repository ecdata, https://github.com/JohnCremona/ecdata: the curves, the aplist and the labels.
- A. O. L. Atkin and J. Lehner, Hecke operators on Gamma0(m), 1970: a_p = -w_p for p || N and a_p = 0 for p^2 | N.
- J. Sturm, On the congruence of modular forms, 1987: the bound k/12 [SL_2(Z) : Gamma0(N)].
- R. Livne, Cubic exponential sums and Galois representations, 1987: the criterion with a non-cubic set of Frobenius elements.
- J. H. Silverman, The arithmetic of elliptic curves, chapter VII: the reduction types, the a_p at the bad primes, and the test of minimality by the valuations of Delta, c4 and c6.

## What the run does not do

- It is a computation, not a proof. An agreement is evidence, and only a certificate that Lean checks makes a theorem (spec 13.4).
- It does not prove the modularity of a curve. The Sturm bound compares two modular forms, and the L-series of E is not known to be one without the theorem of modularity or the criterion of Livne.
- It does not compute the newforms. It reads their a_p from the aplist and checks them only against the curves. It does not check that the aplist comes from modular symbols.
- It does not reach the Sturm bound for the classes that are not Sturm-complete, because the aplist stops at p = 97.
- It does not prove that the traces of rho_f are even, and it does not have the method of Serre for the classes with no rational point of order 2.
- It does not compute the conductor by the algorithm of Tate. It reads N from the data and checks it only through the primes of the discriminant and the reduction types.
- It runs in the lgl binary, not in a container with pinned images, and it uses no network. The data was read from GitHub before the run, and the record gives the sha256 of each file. It uses no random numbers.
