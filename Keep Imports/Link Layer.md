[[Keep/Colour/BLUE]] [[Keep/Attachments]] [[Keep/Archived]] 

1. Hosta nd routers are nodes links are wired or wirelss
2. it response for transfer the datagram from one node to physically adjacent node over a link(wire or wireless)
3. ethernet,802.11 two protocol
4. in the form of datagram
5. encapsulate the frame from datgram(from network layer),MAC addressuesd in frame headers to identify the source,dest....., flow control,error detection,..
6.1  sending site:encapsulates the datgram into frame and add the error checking ,checking bits ,RDT,flow control 
6.2 Recive site:looks for error ,rdt,flow control ,extract the datagram,passes to upper layer at receiving side
8. it is implemented in both software and hardware layers and implemented inNIC (aka adaptor)


Single bit error one error vantha athu 100 nu send 101 nu received na single bit error
Burst errors na more than one single error 10100 to 01001 ,we cannot predict the where is the error


ERROR DETECTION

Single bit error na parity vachi check panuradhu, and CRC na burst error vachi detect



1. SPC(single bit error)only change to find the single bit error- even parity no of one is even,it's less cost,(110 na ,1100 nu aagakum illa 1110 na 11101 nu last ta one na add pan,11101 na change aagi 01101 nu iruthu 011011),count one even na irutha add zero

 parity -> count of 1s should be even
 Even parity
 10100-> 10100(0) -> na crt but 11100(0) nu iruthuchuna athu corrupted
 Odd parity -> 10101 -> 10101(1) -> na 101011 nu crt aana 100011 na corrupted





CHECKSUM
2. CRC
Cyclic Redundancy check,
1. Data,2. CRC generator 3.crc bits,
CRC generator n bits and CRC bits is n-1 bits
PICS:1
First data la Ula potu next CRC generator ra divide potu ,next CRC generator la n bit iruthuchu na athula n-1 nu potu data la sethu divide pannanum athuvum [xor divide( 1 and 1 na zero ,zero and zero ana zero) others are one ], last ta remainder la enna varuthoo atha data la add Pani send it.

2. Receiver la CRC generator ra vachi divide it the balance zero it is non corrupt



CORRECTION and DETECTION
Hamming codes FOR Single bit error
2 PICS









![[1670500669912.787637836.png]]

![[1670501893517.756030181.png]]

![[1670502643253.1204970017.png]]