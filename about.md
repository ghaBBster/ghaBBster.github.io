# Work Experience: Entry-Level Reverse Engineer / Malware Analyst (6 months)

## First Projects Under Mentorship

### Project 1: Analysis of Simple Password Stealer "BasicGrab" (October 2024)

**Task:** First real analysis under senior analyst supervision - simple browser password stealer.

**What I did:**
- **Initial triage:** Used VirusTotal, checked basic PE properties in PEStudio
- **Behavioral analysis:** Ran in isolated VM, monitored through Process Monitor
- **Basic static analysis:** Opened in IDA Free, studied strings and imports under mentor guidance

**What I learned:**
- Basics of PE structure (sections, imports, strings)
- How password stealers work with Chrome/Firefox profiles
- Basic Windows API functions (CreateFile, ReadFile, CryptUnprotectData)

**Challenges:** Got lost in assembly code, didn't immediately understand the connection between API calls and functionality. Mentor helped understand the call flow.

**Result:** Created my first analysis report (8 pages) describing behavior and IOCs. Received feedback: *"Good attention to detail, but needs more practice with assembly."*

---

### Project 2: Unpacking Simple UPX-packed Sample (November 2024)

**Task:** Learn packing/unpacking basics with a simple example.

**Learning process:**
- **Theory:** Studied what packing is, why it's used, how UPX works
- **Detection:** Learned to identify packed files through entropy, PEiD
- **Manual unpacking:** Performed manual unpacking in x64DBG under senior guidance

**Steps performed:**
1. Loaded in x64DBG, found pushad instruction
2. Set breakpoint on popad, stepped through  
3. Found original entry point, dumped process
4. Used Import REConstructor for fixing imports

**Challenges:** Got confused in debugger interface, didn't understand the difference between VA and RVA. Took several attempts and explanations.

**Achievement:** Successfully unpacked first sample independently! Felt like a real reverse engineer.

---

### Project 3: Analysis of Suspicious PowerShell Script (December 2024)

**Task:** Analysis of obfuscated PowerShell loader (entry-level complexity).

**Obfuscation techniques:**
- Multi-level Base64 encoding
- String concatenation and character replacement
- Invoke-Expression chains

**My approach:**
- **Manual deobfuscation:** Step-by-step decryption of each level in PowerShell ISE
- **Dynamic analysis:** Used PowerShell transcript logging for monitoring
- **Final payload:** Discovered download and execute .NET binary

**Learning curve:** First time working with PowerShell analysis. Spent a lot of time understanding PowerShell syntax and built-in functions.

**Outcome:** Successfully deobfuscated script, extracted download URLs, created simple network IOCs. Mentor praised patience in manual deobfuscation.

---

### Project 4: Linux Kernel Rootkit Analysis (January 2025)

**Task:** Analyze simple loadable kernel module (LKM) rootkit that hides processes and files on Linux system.

**What I did:**
- **Kernel module inspection:** Examined rootkit.ko file structure, analyzed ELF headers and symbol tables
- **Static analysis in IDA:** Reverse engineered key functions that hook system calls
- **Dynamic analysis:** Loaded module in isolated Linux VM, monitored kernel behavior through ftrace and /proc/kallsyms
- **Hook detection:** Identified modifications to sys_call_table, getdents64 hooking for file hiding

**Technical details:**
```c
// Discovered hooking mechanism
original_getdents64 = (void *)sys_call_table[__NR_getdents64];
sys_call_table[__NR_getdents64] = (unsigned long *)hooked_getdents64;
```

**What I learned:**
- **Kernel internals:** Understanding of system call table, kernel symbols, module loading process
- **Linux security:** How rootkits operate at kernel level, privilege escalation techniques
- **Syscall hooking:** Methods for intercepting system calls (sys_call_table modification, kprobes)
- **Detection techniques:** Comparing syscall addresses, analyzing /proc/modules, checking for hidden entries

**Challenges:** 
- First time working with kernel-level code - steep learning curve
- Understanding pointer manipulation in kernel space was difficult
- Kernel debugging crashes required multiple VM restores
- Had to learn kernel module compilation and symbol resolution

**Tools used:**
- **IDA Pro:** For static analysis of kernel module
- **GDB with kernel debugging:** For dynamic analysis and breakpoint setting
- **objdump/readelf:** For inspecting ELF structure
- **Volatility:** For memory forensics and hidden process detection
- **ftrace/kprobes:** For tracing kernel function calls

**Outcome:** 
- Successfully identified hooking mechanisms and hidden processes
- Created detection script that compares syscall table against known good values
- Wrote 12-page technical report on rootkit functionality
- Developed understanding of kernel-level malware that will help with future rootkit analysis

**Mentor feedback:** *"Impressive for first kernel-level analysis. Good understanding of low-level concepts. Continue studying Linux kernel internals."*

---

### Side Project: Contributing to Custom Unix-like Kernel Development (Ongoing)

**Background:** Started contributing to educational microkernel project to better understand OS internals for malware analysis work.

**Contributions:**
- **Process scheduler improvements:** Implemented basic priority-based scheduling algorithm
- **System call interface:** Added several POSIX-compatible system calls (fork, exec, wait)
- **Memory management:** Worked on page allocation and virtual memory mapping
- **Debugging support:** Added kernel logging and panic handling mechanisms

**Code example - Simple syscall implementation:**
```c
// sys_getpid implementation
asmlinkage long sys_getpid(void) {
    struct task_struct *current_task = get_current();
    return current_task->pid;
}

// Syscall table entry
[__NR_getpid] = sys_getpid,
```

**What this teaches me:**
- **Deep OS understanding:** How processes, memory, and system calls work at fundamental level
- **Security implications:** Understanding privilege boundaries helps identify kernel exploits
- **Malware perspective:** Knowing how OS works helps predict what malware can/cannot do
- **Rootkit detection:** Understanding legitimate kernel operations makes anomalies more obvious

**Technical skills developed:**
- **C programming:** Low-level system programming, pointer arithmetic, memory management
- **Assembly:** x86/x86_64 assembly for context switching and interrupt handling
- **Debugging:** Kernel debugging with GDB, analyzing kernel panics and crashes
- **Build systems:** Working with Makefiles, cross-compilation, bootloader integration

**Relevance to malware analysis:**
- Understanding syscall flow helps analyze syscall hooking rootkits
- Knowledge of kernel structures aids in memory forensics
- Familiarity with legitimate kernel operations helps spot malicious modifications
- Experience with kernel debugging translates to rootkit dynamic analysis

**Repository:** Contributing to open-source educational kernel project (500+ lines of code contributed)

**Learning resources used:**
- "Linux Kernel Development" by Robert Love
- "Understanding the Linux Kernel" by Bovet & Cesati
- OSDev wiki and forums
- Linux kernel source code reading

**Future goals:**
- Implement basic file system support
- Add network stack fundamentals
- Study modern kernel security features (KASLR, SMEP, SMAP)
- Apply knowledge to advanced rootkit analysis

---

## Skills and Tools Being Learned

### Basic Technical Skills (in progress)

- **PE Analysis:** Understand basic structure, can find entry point, imports, strings
- **Assembly Reading:** Slowly but surely read simple x86/x64 code, understand basic instructions
- **Debugging:** Basic navigation in x64DBG, can set breakpoints, step through code
- **Static Analysis:** IDA Free - know main functions, but often need help with complex analysis

### Malware Analysis Basics (beginner level)

- **Triage Skills:** Can perform initial assessment through online tools and PE utilities
- **Behavioral Monitoring:** Comfortable with Process Monitor, Registry monitoring, basic file analysis
- **VM Management:** Learned to work with VMware snapshots, isolated networking
- **Documentation:** Write structured reports, but still simple and short

### Programming Skills (learning)

- **Python:** Wrote several simple scripts (50-100 lines), understand basics
- **YARA:** Created 5 basic rules under supervision, understand pattern matching
- **Batch/PowerShell:** Basic automation scripts for routine tasks
- **Assembly:** Read simple code, but complex constructs still challenging
- **C/C++:** Learning through kernel development project, comfortable with pointers and memory management
- **Shell scripting:** Basic bash scripts for Linux automation and analysis tasks

---

## Mini-projects and Learning Exercises

### Hash Extractor Script (Python, 75 lines)

First independent script for extracting file hashes:
- Calculates MD5, SHA1, SHA256 for batch files
- Simple command-line interface
- **Feedback:** Colleague used it for quick IOC generation

### Basic Strings Analyzer (Python, 120 lines)

Script for enhanced string analysis:
- Filters out common Windows strings
- Highlights suspicious patterns (URLs, IPs, registry keys)
- Exports results to CSV format
- **Learning:** Improved understanding of regex and file I/O

### VM Automation Scripts (Batch, 50 lines)

Simple scripts for routine VM tasks:
- Automatic snapshot creation/restoration
- Log collection and cleanup
- **Impact:** Saves 15-20 minutes of daily routine

---

## Education and Development

### Completed Materials

- **"Practical Malware Analysis" book:** Read first 8 chapters, doing exercises
- **Online tutorials:** Malware Unicorn workshops, YouTube tutorials on IDA
- **Internal training:** Weekly sessions with team mentor

### Current Learning Challenges

- **Assembly understanding:** Read code slowly, especially difficult with indirect calls and pointer arithmetic
- **Tool proficiency:** Know basic IDA/x64DBG functions, but advanced features still a mystery
- **Pattern recognition:** Don't always see connections between code patterns and malware behavior

### Practical Experience Stats

- **Analyzed 15+ samples** under supervision (mostly simple stealers, downloaders)
- **Created 5 YARA rules** with mentor's help
- **Documented 8 cases** in internal knowledge base
- **Participated in 3 team meetings** as observer/junior contributor
- **Analyzed 1 Linux kernel rootkit** with mentor guidance
- **Contributed 500+ lines** to open-source kernel project

---

## Current Achievements Over 6 Months

| Month | Achievements |
|-------|------------|
| **October 2024 (Month 1)** | Set up personal lab environment<br>Completed first supervised analysis<br>Learned PE structure basics |
| **November 2024 (Month 2)** | First successful manual unpacking<br>Started writing analysis reports<br>Learned x64DBG basics |
| **December 2024 (Month 3)** | Analyzed first script-based malware<br>Improved Python scripting skills<br>Created first useful automation tool |
| **January 2025 (Month 4)** | More independent analysis work<br>Better understanding of malware families<br>Improved documentation quality<br>First Linux kernel rootkit analysis |
| **February 2025 (Month 5)** | First semi-independent investigation<br>Started contributing to team knowledge base<br>Developed confidence in basic techniques |
| **March 2025 (Month 6)** | Leading analysis on simple cases<br>Mentoring new intern<br>Planning next learning goals |

---

## Feedback Received

### From Senior Analyst:
> - *"Shows good curiosity and willingness to learn"*
> - *"Documentation skills improving rapidly"*
> - *"Needs more practice with complex static analysis"*
> - *"Good attention to detail in behavioral analysis"*

### From Team Lead:
> - *"Progressing well for entry level"*
> - *"Should focus on fundamentals before advanced topics"*
> - *"Good team player, asks intelligent questions"*

### Self-assessment:
- Feel progress, but understand there's still a lot I don't know
- Sometimes overwhelmed by complex samples
- Gaining confidence in basic tasks
- Excited about learning more advanced techniques

---

## Near-term Goals (next 6 months)

### Technical Goals

- **Assembly fluency:** Want to read assembly code without constant help
- **Advanced unpacking:** Learn techniques for more complex packers  
- **IDA proficiency:** Master IDAPython scripting for automation
- **Network analysis:** Dive deeper into protocol analysis and C2 communications

### Project Goals

- **Independent analysis:** Lead 2-3 cases completely independently
- **Tool development:** Create useful tool for team usage
- **Knowledge sharing:** Write internal guide on learned topic
- **Mentoring:** Help next newcomer on the team

### Learning Plan

- **Structured learning:** Finish "Practical Malware Analysis" book
- **Hands-on practice:** Daily analysis on different malware types
- **Certification prep:** Start preparing for entry-level certification
- **Conference attendance:** Attend local security meetup

---

## Motivation and Perspectives

### Why I Chose This Field

Always interested in cybersecurity, fascinated by reverse engineering process. Love the intellectual puzzle-solving aspect.

### What I Enjoy Most

- The moment when I finally understand how obfuscated code works
- Satisfaction from successful unpacking
- Team collaboration and knowledge sharing

### Current Interests

- Studying evolution of modern malware families
- Reading threat intelligence reports
- Following security researchers on Twitter

### Long-term Vision

- **In 1 year:** Want to become confident junior analyst
- **In 2-3 years:** Specialize in advanced persistent threats or mobile malware analysis

### Readiness to Grow

Understand I'm at the very beginning of the learning curve, but motivated to continue development. Ready to invest time in continuous learning and practice.

---

## Additional Activities

### Community Involvement

- Participate in local CTF events (mainly learning experience so far)
- Read malware analysis blogs and Twitter feeds
- Started keeping personal learning journal

### Side Projects

- Setting up home lab for personal practice
- Planning to create malware analysis blog to document learning journey
- Experimenting with different analysis tools and techniques

---

## Conclusion

Although experience is still limited, I'm motivated to continue learning and development in this fascinating field. Ready to take on challenges and grow as a professional under the guidance of an experienced team.

---

### Key Skills
`Malware Analysis` | `IDA Pro` | `x64DBG` | `Python Scripting` | `YARA Rules` | `PE Analysis` | `Assembly Reading` | `VM Management` | `Behavioral Analysis` | `Documentation` | `Linux Kernel Analysis` | `C Programming` | `System Calls` | `Rootkit Analysis` | `GDB Debugging`

### Analyzed Families
`Password Stealers` | `Downloaders` | `PowerShell Malware` | `Packed Samples` | `Simple RATs` | `Linux Kernel Rootkits` | `LKM Malware`

### Toolset
`IDA Free` | `x64DBG` | `Process Monitor` | `VMware` | `VirusTotal` | `PEStudio` | `PEiD` | `PowerShell ISE` | `Python` | `GDB` | `Volatility` | `ftrace` | `objdump` | `readelf`
