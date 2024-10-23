<h1>American Fuzzy Lop</h1>

<h2>Description</h2>
This repository shows the progress of running American Fuzzy Lop (AFL) fuzzer and analyzing software vulnerability.

<h2>Project Overview</h2>

<b>Targeted Software:</b> 
- Target Software: libpng
- Targeted Version: v1.4.1. git
- Size: approx 676 KB
- Code Repository: https://github.com/glennrp/libpng
- Conducted Date: 23/10/202
- Tested Harness: libpng-harness.c
  
<b>Summary:</b> 
- Total Fuzzing Duration: 4 hrs, 2 min, 44 sec
- Paths and Crashes: 115 Paths, 39 unique crashes
- Coverage: The fuzzer achieved a map coverage of approximately 67.8% with a density 
of 0.52%.
- Performance: The execution speed of the fuzz is approximately 41.60 per second.
- Findings: 39 unique crashes are revealed. Some of the test cases yielded 110 unique 
findings.


<br />
<b>Screen Capture (run time: 1 hrs, 15 min, 15 sec)</b>
<img src="https://i.imgur.com/ecRUT7e.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<b>Screen Capture (run time: 2 hrs, 36 min, 58 sec)</b>
<img src="https://i.imgur.com/HbLvGj2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<b>Final Result (run time: 4 hrs, 2 min, 44 sec)</b>
<img src="https://i.imgur.com/AsiT623.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
<b>39 Unique Crashes</b>
<img src="https://i.imgur.com/llbCMJ0.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
<br/>
<b>Analyzing first crash : id:000000,sig:06,src:000000,time:1716,op:flip1,pos:12</b> 
<br/>
<img src="https://i.imgur.com/KNuN8jV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
(1) Error: Global buffer overflow occurred at address 0x000000539cb3. (using Address Sanitizer) Read operation of size 64 was performed. This read operation went past the bounds of a global buffer.

(2) cause of the vulnerability: When libpng attempts to read and process this oversized or malformed chunk, it exceeds the boundaries of the buffer allocated for chunk data, leading to a global buffer overflow.

(3) Location of the vulnerability: The error occurred within the libpng library, specifically in the png_format_buffer function located in Source file: pngerror.c at line 184. It was triggered during the process of checking PNG chunk names in the png_check_chunk_name function, which is part of the png_read_chunk_header function.

<br/>
<b>Location details:</b>
<img src="https://i.imgur.com/JB9vrv2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
<br/>
<b>Exploitability details:</b>
<img src="https://i.imgur.com/m8mbFDL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br/>
