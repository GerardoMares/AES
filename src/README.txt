Dylan Soechting and Gerardo Mares

Our implementation uses the standard java compiler i.e. run "javac AES.java" if
you want to compile the code, and then run "java AES --mode $MODE" to execute,
where $MODE is either 'encrypt' or 'decrypt'. Place your desired input in input.txt
and change the key with the byte array in the code byte[] key on line 221.
Place encrypted data in encrypted.txt for it to go through the decryption process.

The output for encryption will be sent to encrypted.txt and the output for
decryption will be sent to decrypted.txt.

AES iterates through four steps: addRoundKey, subBytes, shiftRows, and mixColumns.
Those four steps are one round of the encryption process. The amount of rounds is
determined by the length of the key, for example a 128 bit key requires 10 rounds.

addRoundKey requires an expanded key. The expanded key is acquired by XORing words
in the chunk of four with the previous word in the same chunk and a word from the
previous chunk in the corresponding word position. The first word of each chunk of
four words is unique in the fact that the previous byte is from the previous word
and goes through some gFunction, which rotates the word, runs it through the
subByte function, and then runs it through the rounded constant function
(implemented with a lookup table).

The block of input text is then XOR'ed with each word in the expanded key.

subBytes takes the hex value and uses the first and last digit of the hex byte
to index in to an SBox lookup table and then XORs the original byte with the value
found from the look up table.

shiftRows takes a 4x4 block of bytes and shifts each row to the left depending on
the row number. For example, row 0 gets shifted to the left 0 times, row 1 gets
shifted to the left 1 time etc...

mixColumns applies galois multiplication to each byte in the state array by a
value looked up in a table based on the galois value for that byte in the state
calculated by a lookup in our galois table.

For decryption, inverse functions are applied to most of the steps in each round.
For subBytes and mixColumns, the algorithm remains the same, with the exception
that a different look up table is used. shiftRows shifts the rows to the right
instead of the left. addRoundKey keeps the same functionality as encryption.
