Data size truth table
=============
|Name|Register bit|Description                                               |
|:--:|:-----------|:---------------------------------------------------------|
|B   |0...7       |Byte (1 Byte integer)                                     |
|W   |0...15      |Word (2 Byte integer)                                     |
|D   |0...31      |Double Word (4 Byte integer)                              |
|Q   |0...63      |Quad Word (8 Byte integer)                                |
|O   |0...127     |Octa Word (16 Byte integer)                               |
|HF  |0...15      |Half precision floating points (IEEE 754 format, 2 Byte)  |
|SF  |0...31      |Single precision floating points (IEEE 754 format, 4 Byte)|
|DF  |0...63      |Double precision floating points (IEEE 754 format, 8 Byte)|
|QF  |0...127     |Quad precision floating points (IEEE 754 format, 16 Byte) |
|HV  |0...63      |Half size vector (8 Byte, 1~8 datas in vector)            |
|V   |0...127     |Full size vector (16 Byte, 1~16 datas in vector)          |

Register table
=============
Each register size is 128 bits
<br>
|Register|Number of banks|Usage                           |
|:-------|:-------------:|:-------------------------------|
|R0      |1              |Zero constant register          |
|R1...R27|16             |General purpose register        |
|R28/BP  |16             |Base pointer register           |
|R29/FP  |16             |Frame pointer register          |
|R30/SP  |16             |Stack pointer register          |
|R31/PC  |1              |Program counter register        |
|CR      |16             |Control register                |
|FPCR    |16             |Floating point control register |
|VCR     |16             |Vector Control register         |
|EVBR    |1              |Exception Vector base register  |

CR register bit table
=============
|Name|CR bits  |Usage                       |
|:---|:-------:|:---------------------------|
|NF  |0        |Negative flag               |
|ZF  |1        |Zero flag                   |
|CF  |2        |Carry flag                  |
|VF  |3        |Overflow flag               |
|EF  |4        |Equals flag                 |
|GF  |5        |Greater flag                |
|NaNF|6        |Not a Number flag           |
|INFF|7        |Infinity flag               |
|UOF |8        |Unordered flag              |
|IE  |9        |Interrupt enable flag       |
|PVL |10...11  |Privileged Level            |
|IB  |16...19  |Integer register bank       |
|FB  |20...23  |Floating point register bank|
|VB  |24...27  |Vector register bank        |
|VC  |120...127|Version code                |

Address Size/PC Wrap/Stack Wrap/Frame wrap formats
=============
|Inst.Bit/Data Bit|127...64    |63...32    |31...16    |15...8    |7...0    |Description                     |
|:----------------|:----------:|:---------:|:---------:|:--------:|:-------:|:-------------------------------|
|0b000            |BP[127...64]|BP[63...32]|BP[31...16]|BP[15...8]|A[7...0] |120 bit Bank + 8 bit Address    |
|0b001            |BP[127...64]|BP[63...32]|BP[31...16]|A[15...8] |A[7...0] |112 bit Bank + 16 bit Address   |
|0b010            |BP[127...64]|BP[63...32]|A[31...16] |A[15...8] |A[7...0] |96 bit Bank + 32 bit Address    |
|0b011            |BP[127...64]|A[63...32] |A[31...16] |A[15...8] |A[7...0] |64 bit Bank + 64 bit Address    |
|0b100            |A[127...64] |A[63...32] |A[31...16] |A[15...8] |A[7...0] |128 bit Linear Address          |
<br>
BP: PC register (Code, PC Wrap) or Base pointer register (Data) or Stack poinster register (Stack, Stack Wrap) or Frame poinster register (Frame Wrap)

Integer data size formats
=============
|Inst.Bit/Data Bit|127...64    |63...32    |31...16    |15...8    |7...0    |Description                     |
|:----------------|:----------:|:---------:|:---------:|:--------:|:-------:|:-------------------------------|
|0b000            |-           |-          |-          |-         |B[7...0] |Byte                            |
|0b001            |-           |-          |-          |W[15...8] |W[7...0] |Word                            |
|0b010            |-           |-          |D[31...16] |D[15...8] |D[7...0] |Double Word                     |
|0b011            |-           |Q[63...32] |Q[31...16] |Q[15...8] |Q[7...0] |Quad Word                       |
|0b100            |O[127...64] |O[63...32] |O[31...16] |O[15...8] |O[7...0] |Octa Word                       |
<br>
- : don't care

Floating point data size formats
=============
|Inst.Bit/Data Bit|127...64    |63...32    |31...16    |15...0    |Description                     |
|:----------------|:----------:|:---------:|:---------:|:--------:|:-------------------------------|
|0b00             |-           |-          |-          |HF[15...0]|Half precision floating points  |
|0b01             |-           |-          |SF[31...16]|SF[15...0]|Single precision floating points|
|0b10             |-           |DF[63...32]|DF[31...16]|DF[15...0]|Double precision floating points|
|0b11             |QF[127...64]|DF[63...32]|DF[31...16]|DF[15...0]|Quad precision floating points  |
<br>
- : don't care

Full size integer vector formats
=============
|Inst.Bit/Vector Bit|127...120     |119...112     |111...104     |103...96     |95...88     |87...80     |79...72     |71...64     |63...56     |55...48     |47...40     |39...32     |31...24     |23...16     |15...8     |7...0     |Name|Description                     |
|:------------------|:------------:|:------------:|:------------:|:-----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:---------:|:--------:|:--:|:-------------------------------|
|0b000              |B15[7...0]    |B14[7...0]    |B13[7...0]    |B12[7...0]   |B11[7...0]  |B10[7...0]  |B9[7...0]   |B8[7...0]   |B7[7...0]   |B6[7...0]   |B5[7...0]   |B4[7...0]   |B3[7...0]   |B2[7...0]   |B1[7...0]  |B0[7...0] |BV  |Byte vector                     |
|0b001              |W7[15...8]    |W7[7...0]     |W6[15...8]    |W6[7...0]    |W5[15...8]  |W5[7...0]   |W4[15...8]  |W4[7...0]   |W3[15...8]  |W3[7...0]   |W2[15...8]  |W2[7...0]   |W1[15...8]  |W1[7...0]   |W0[15...8] |W0[7...0] |WV  |Word vector                     |
|0b010              |D3[31...24]   |D3[23...16]   |D3[15...8]    |D3[7...0]    |D2[31...24] |D2[23...16] |D2[15...8]  |D2[7...0]   |D1[31...24] |D1[23...16] |D1[15...8]  |D1[7...0]   |D0[31...24] |D0[23...16] |D0[15...8] |D0[7...0] |DV  |Double Word vector              |
|0b011              |Q1[63...56]   |Q1[55...48]   |Q1[47...40]   |Q1[39...32]  |Q1[31...24] |Q1[23...16] |Q1[15...8]  |Q1[7...0]   |Q0[63...56] |Q0[55...48] |Q0[47...40] |Q0[39...32] |Q0[31...24] |Q0[23...16] |Q0[15...8] |Q0[7...0] |QV  |Quad Word vector                |
|0b100              |O0[127...120] |O0[119...112] |O0[111...104] |O0[103...96] |O0[95...88] |O0[87...80] |O0[79...72] |O0[71...64] |O0[63...56] |O0[55...48] |O0[47...40] |O0[39...32] |O0[31...24] |O0[23...16] |O0[15...8] |O0[7...0] |OV  |Octa Word vector                |

Full size floating point vector formats
=============
|Inst.Bit/Vector Bit|127...120     |119...112     |111...104     |103...96     |95...88     |87...80     |79...72     |71...64     |63...56     |55...48     |47...40     |39...32     |31...24     |23...16     |15...8     |7...0     |Name|Description                            |
|:------------------|:------------:|:------------:|:------------:|:-----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:---------:|:--------:|:--:|:--------------------------------------|
|0b00               |HF7[15...8]   |HF7[7...0]    |HF6[15...8]   |HF6[7...0]   |HF5[15...8] |HF5[7...0]  |HF4[15...8] |HF4[7...0]  |HF3[15...8] |HF3[7...0]  |HF2[15...8] |HF2[7...0]  |HF1[15...8] |HF1[7...0]  |HF0[15...8]|HF0[7...0]|HFV |Half precision floating points vector  |
|0b01               |SF3[31...24]  |SF3[23...16]  |SF3[15...8]   |SF3[7...0]   |SF2[31...24]|SF2[23...16]|SF2[15...8] |SF2[7...0]  |SF1[31...24]|SF1[23...16]|SF1[15...8] |SF1[7...0]  |SF0[31...24]|SF0[23...16]|SF0[15...8]|SF0[7...0]|SFV |Single precision floating points vector|
|0b10               |DF1[63...56]  |DF1[55...48]  |DF1[47...40]  |DF1[39...32] |DF1[31...24]|DF1[23...16]|DF1[15...8] |DF1[7...0]  |DF0[63...56]|DF0[55...48]|DF0[47...40]|DF0[39...32]|DF0[31...24]|DF0[23...16]|DF0[15...8]|DF0[7...0]|DFV |Double precision floating points vector|
|0b11               |QF0[127...120]|QF0[119...112]|QF0[111...104]|QF0[103...96]|QF0[95...88]|QF0[87...80]|QF0[79...72]|QF0[71...64]|QF0[63...56]|QF0[55...48]|QF0[47...40]|QF0[39...32]|QF0[31...24]|QF0[23...16]|QF0[15...8]|QF0[7...0]|QFV |Quad precision floating points vector  |

Half size integer vector formats
=============
|Inst.Bit/Vector Bit|63...56     |55...48     |47...40     |39...32     |31...24     |23...16     |15...8     |7...0     |Name|Description                     |
|:------------------|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:---------:|:--------:|:--:|:-------------------------------|
|0b000              |B7[7...0]   |B6[7...0]   |B5[7...0]   |B4[7...0]   |B3[7...0]   |B2[7...0]   |B1[7...0]  |B0[7...0] |HBV |Half size Byte vector           |
|0b001              |W3[15...8]  |W3[7...0]   |W2[15...8]  |W2[7...0]   |W1[15...8]  |W1[7...0]   |W0[15...8] |W0[7...0] |HWV |Half size Word vector           |
|0b010              |D1[31...24] |D1[23...16] |D1[15...8]  |D1[7...0]   |D0[31...24] |D0[23...16] |D0[15...8] |D0[7...0] |HDV |Half size Double Word vector    |
|0b011              |Q0[63...56] |Q0[55...48] |Q0[47...40] |Q0[39...32] |Q0[31...24] |Q0[23...16] |Q0[15...8] |Q0[7...0] |HQV |Half size Quad Word vector      |

Half size floating point vector formats
=============
|Inst.Bit/Vector Bit|63...56     |55...48     |47...40     |39...32     |31...24     |23...16     |15...8     |7...0     |Name|Description                                      |
|:------------------|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:---------:|:--------:|:--:|:------------------------------------------------|
|0b00               |HF3[15...8] |HF3[7...0]  |HF2[15...8] |HF2[7...0]  |HF1[15...8] |HF1[7...0]  |HF0[15...8]|HF0[7...0]|HHFV|Half size Half precision floating points vector  |
|0b01               |SF1[31...24]|SF1[23...16]|SF1[15...8] |SF1[7...0]  |SF0[31...24]|SF0[23...16]|SF0[15...8]|SF0[7...0]|HSFV|Half size Single precision floating points vector|
|0b11               |DF0[63...56]|DF0[55...48]|DF0[47...40]|DF0[39...32]|DF0[31...24]|DF0[23...16]|DF0[15...8]|DF0[7...0]|HDFV|Half size Double precision floating points vector|

Single scalar in integer vector formats
=============
|Inst.Bit|Name|Description    |
|:-------|:--:|:--------------|
|0b0nnnn |Bn  |Byte #n        |
|0b10nnn |Wn  |Word #n        |
|0b110nn |Dn  |Double Word #n |
|0b1110n |Qn  |Quad Word #n   |
|0b11110 |O0  |Octa Word #0   |

Single scalar in floating point vector formats
=============
|Inst.Bit|Name|Description                         |
|:-------|:--:|:-----------------------------------|
|0b0nnn  |HFn |Half precision floating points #n   |
|0b10nn  |SFn |Single precision floating points #n |
|0b110n  |DFn |Double precision floating points #n |
|0b1110  |QFn |Quad precision floating points #n   |
