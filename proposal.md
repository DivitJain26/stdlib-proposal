# Add a title*
[RFC]: Add BLAS bindings and implementations for linear algebra (Draft)
---

# Your Background

#### Full name*
Divit Jain

### University status*
Yes

### University name
MIT ADT University, Pune, India

### University program
Bachelor of Technology in Computer Science and Engineering

### Expected graduation
2027

### Short biography*

### Timezone*
Indian Standard Time ( IST ), UTC+5:30

### Contact details* 
email:divit26@gmail.com,github:[DivitJain26](https://github.com/DivitJain26)
---

# Programming Experience

### Platform*
Linux

### Editor*
My preferred code editor is Visual Studio Code (VSCode). I like it for its simplicity, and it fulfills all my development requirements. Also provides good integration with WSL, which allows me to work easily in a Linux environment while developing on Windows.

### Programming experience*
Pursuing computer science marked my programming journey. I started with the basics of HTML and CSS,  gradually moving into component-based UI development with React.js but that was just the surface.

I wanted to know what triggers when you click a button,how the request travels and gets fulfilled, which drove me to explore backend development.
I picked Node.js and Express.js where I dug into concepts like RESTful API, microservices architecture, and database management. I also have experience with C and C++ which taught me a lot about low level programming. 

With the rapid rise of Artificial Intelligence, I expanded into Python and the mathematics behind Machine Learning, Currently  m interested in built application to target real world problem that can be solved with AI

### Projects:
- **VAK:** Demo of real time comment moderation for social meda, uses an SVM for toxic comment detection. Built with Next.js

	[[GitHub]](https://github.com/DivitJain26/vak)
	[[Live Demo]](Vak-eosin.vercel.app)

- **Aluminate:** Alumni connection platform Full-stack app built on the MERN stack, enabling students and alumni to connect

	[[GitHub]](https://github.com/DivitJain26/Aluminate.git)
	[[Live Demo]](https://aluminate-syvf.onrender.com/)

### JavaScript experience*
JavaScript was my first programming language. I started my journey with web development, and learning JavaScript helped me understand the logic behind the applications.

I primarily use JavaScript for building backend systems and API endpoints. I started using Node.js and Express.js for this project, and it completely shifted my perspective on JavaScript. Through them, I learned about request handling, REST APIs, and asynchronous programming using async/await.

My favorite feature of JavaScript is its flexibility and portability. I compiled my first JavaScript code in the browser, and it fascinates me how the language started as a tool for adding simple animations to web pages and has evolved into a powerful platform. With runtimes like Node.js and Bun, and with TypeScript providing strong typing, JavaScript has become a popular choice for building backend systems.

I also like how JavaScript’s syntax is relatively simple like Python, while still having some strictness similar to Java or C++. It is not perfect, but with TypeScript the ecosystem becomes very robust.

My least favorite aspect of JavaScript is that objects and arrays are mutable and passed by reference, which can sometimes lead to unexpected behavior if not handled carefully.

### Node.js experience*
I began exploring backend development with Node.js in my first year, gaining knowledge about server architecture and web protocols needed for a scalable backend system.
Using Express.js I have built RESTful APIs and implemented features like authentication systems, payment gateway integrations, and CRUD operations. 

### C/Fortran experience*
I was introduced to C programming by my University in my first year, being called the mother of all languages. It helped me grasp low level concepts like memory management, types and how programs interact with system resources.
Later, I learned C++, where I became familiar with object-oriented programming concepts.

I do not currently have experience with Fortran, but I understand it for the purposes of this project, I am also open to learning it more as needed while working on the project.

### Interest in stdlib*

### Version control*
Yes

### Contributions to stdlib*
[Open PRs](https://github.com/stdlib-js/stdlib/issues?q=state%3Aopen%20is%3Apr%20author%3A%40me)

[Merged PRs](https://github.com/stdlib-js/stdlib/issues?q=state%3Amerged%20is%3Apr%20author%3A%40me)

**These Includes**

## PRs
### BLAS Routines
- [feat: add `blas/base/cgbmv` #10492](https://github.com/stdlib-js/stdlib/pull/10492) (open)
	- Added JS implementations of `cgbmv`.
	- Implemented band matrix packing aligening with MKL storage format, which was missing in open PRs of `sgbmv` and `dgbmv`.

- [feat: add `blas/base/cgemv` #10485](https://github.com/stdlib-js/stdlib/pull/10485) (open)
	- Added JS implementations `cgemv`.
	- Added tests for the conjugate transpose, which was missing in other open PRs of complex valued routines.

### Use string interpolation in JavaScript benchmarks
- [bench: refactor to use string interpolation in array/base/take3d #9053](https://github.com/stdlib-js/stdlib/pull/9053) (merged)
- [bench: refactor to use string interpolation in array/base/take2d #9051](https://github.com/stdlib-js/stdlib/pull/9051) (merged)
- [bench: refactor to use string interpolation in array/base/take-map #9050](https://github.com/stdlib-js/stdlib/pull/9050) (merged)
- [bench: refactor to use string interpolation in array/base/take-indexed2 #9049](https://github.com/stdlib-js/stdlib/pull/9049) (merged)
- [bench: refactor to use string interpolation in array/base/take-indexed #9048](https://github.com/stdlib-js/stdlib/pull/9048) (merged)
- [bench: refactor to use string interpolation in array/base/take #9026](https://github.com/stdlib-js/stdlib/pull/9026) (merged)

### Fix JavaScript lint errors
- [chore: fix JavaScript lint errors (issue #9544) #9546](https://github.com/stdlib-js/stdlib/pull/9546) (merged)
- [chore: fix EditorConfig lint errors #9409](https://github.com/stdlib-js/stdlib/pull/9409) (merged)
- [chore: fix JavaScript lint errors (issue #9334) #9337](https://github.com/stdlib-js/stdlib/pull/9337) (merged)

### Address commit comments for commit
- [chore: address commit comments for commit 9799f77 (issue #9288) #9294](https://github.com/stdlib-js/stdlib/pull/9294) (merged)
- [chore: address commit comments for commit 540a83e (issue #9236) #9242](https://github.com/stdlib-js/stdlib/pull/9242) (merged)
- [chore: address commit comments for commit 8a20a3e (issue #9235) #9241](https://github.com/stdlib-js/stdlib/pull/9241) (merged)

### Others
- [fix(bench): resolve TypeScript declaration lint errors #9320](https://github.com/stdlib-js/stdlib/pull/9320) (open)
- [docs: improve doctests for ndarray instances in ndarray/any #9345](https://github.com/stdlib-js/stdlib/pull/9345) (merged)

## Code Reviews
- [Row-major band matrix packing inconsistency in `dgbmv`](https://github.com/stdlib-js/stdlib/pull/6121#discussion_r2918859963)
- [Row-major band matrix packing inconsistency in `sgbmv`](https://github.com/stdlib-js/stdlib/pull/5928#discussion_r2925124089)
- [Column-major band matrix packing inconsistency in `sgbmv`](https://github.com/stdlib-js/stdlib/pull/5928#discussion_r2925149237)

### stdlib showcase*
I made **Linear Regression Visualizer** allowing users to generate data points, train a model and observe how the regression line converges over time along with the error across training epochs.

This project uses `stdlib` numerical and BLAS utilities including `uniform`, `daxpy`, `ddot`, `dnrm2`, `pow` and `randu` which can be found in [`src/utils/sgdRegression.ts`](https://github.com/DivitJain26/Linear-Regression-Visualizer/blob/04c81ee92da3f7162a389737bfb5b031328cfbe3/src/utils/sgdRegression.ts)

[[GitHub]](https://github.com/DivitJain26/Linear-Regression-Visualizer.git)
[[Live Demo]](https://divitjain26.github.io/Linear-Regression-Visualizer/)

---

# Project Description

### Goals*
This project has been carried forward for the past two years, and several routines have already been implemented (many of them currently have open PRs). The remaining routines are in Level 2 and Level 3 and are mostly complex-valued.

- As discussed with Athan, the top priority is to complete the implementation of real-valued routines. Since most real-valued routines already have JavaScript implementations, I will focus on implementing their corresponding C versions.

- The second priority is complex-valued routines. I will implement both JavaScript and C implementations of those routines.

Fortran and WebAssembly implementations are currently a lower priority. The Fortran implementations are blocked, and the WebAssembly API is relatively complex for general users.

### Why this project?*
I started contributing in stdlib with good first issues. While exploring the repository I noticed this project listed among the pinned issues. I wanted to step out of my comfort zone and take on something relatively more challenging and important for the organization.
Initially, I was not very familiar with BLAS, but as I stareted exploring the issue and reading more about it, I realised its importance. From machine learning algorithms to high performance computing, BLAS plays a fundamental role in many numerical and scientific applications, which fascinated me.

This project provides a great opportunity for me to contribute meaningfully, as it aligns well with my interests and skills. The fact that it has been rigorously worked upon for the past two years makes me more sincere about my contribution to the community. I hope to carry forward the same level of dedication shown by contributors in previous years and help advance the project.
Being a science student, working with matrices and vectors felt natural to me. Earlier, these concepts were limited to textbooks, but working close with them in real implementations has been an immensely valuable learning experience.

### Qualifications*
I believe I am well prepared to contribute to and help lead this project, as I already have meaningful contributions in `blas/base/cgemv` and `blas/base/cgbmv` and along the way I have developed a deep understanding of the BLAS kernels, testing strategies, documentation, and common practices expected by `stdlib`. 

While working on complex-valued BLAS Level 2 routines, I gained exposure to related routines, including real-valued routines and the broader structure of Level 3 operations. 
I find it worth mentioning that in the process of studying band matrix routines I noticed that some open PRs from the previous year’s GSOC had some inconsistency in packing band matrices compared to BLAS MKL, and I improved it in my implementation to ensure it aligns with the official documentation.

My academic background supports this project as well. I have qualified a nationwide examination called [Design and Analysis of Algorithms by NPTEL](https://archive.nptel.ac.in/content/noc/NOC25/SEM2/Ecertificates/106/noc25-cs90/Course/NPTEL25CS90S34540007909204048.pdf) through which I have developed a strong foundation of core algorithms and data structures, and it aids me to analyse complexity of an algorithm and come up with optimization techniques.

In addition, I regularly practice data structures and algorithms on [LeetCode](https://leetcode.com/u/Divit_Jain/), which further strengthens my problem-solving skills and algorithmic thinking.

### Prior art*
The earliest implementation of BLAS can be traced back to 1979, [LINPACK](https://en.wikipedia.org/wiki/LINPACK) and [EISPACK](https://en.wikipedia.org/wiki/EISPACK) were the earliest numerical libraries to provide Fortran based BLAS functionality. Later, [LAPACK](https://www.netlib.org/lapack/explore-html/) became widely adopted due to its better support for modern hardware architectures.
Over time, the focus of numerical computing shifted toward performance optimization. Libraries such as [Intel one API Math Kernel Library (oneMKL)](https://www.intel.com/content/www/us/en/developer/tools/oneapi/onemkl.html), [OpenBLAS](https://github.com/OpenMathLib/OpenBLAS), and [cuBLAS](https://developer.nvidia.com/cublas) emerged to provide highly optimized BLAS implementations for different hardware platforms. Personally for me [Intel one API Math Kernel Library (oneMKL)](https://www.intel.com/content/www/us/en/developer/tools/oneapi/onemkl.html) and [LAPACK](https://www.netlib.org/lapack/explore-html/) has been my Bible for BLAS, I have frequently used them as guides for routine definitions, input parameters, and expected results for my contributions till now.

Python libraries like [NumPy](https://numpy.org/devdocs/building/blas_lapack.html) and [SciPy](https://docs.scipy.org/doc/scipy/reference/linalg.blas.html) provide BLAS wrappers which use foundational libraries like LAPACK and OpenBLAS under the hood.

Within `stdlib` this project has been carried forward by [Aman Bhansali](https://github.com/aman-095) and [Shabareesh Shetty](https://github.com/ShabiShett07), their contributions have been an immense help for me to deepen my understanding of this project and to contribute to it meaningfully.

### Commitment*

### Schedule*
Assuming a 12 week schedule,

- **Community Bonding Period**:

- **Week 1**:

- **Week 2**:

- **Week 3**:

- **Week 4**:

- **Week 5**:

- **Week 6**: (midterm)

- **Week 7**:

- **Week 8**:

- **Week 9**:

- **Week 10**:

- **Week 11**:

- **Week 12**:

- **Final Week**:

### Related issues
[[RFC]: Add BLAS bindings and implementations for linear algebra (tracking issue) #2039](https://github.com/stdlib-js/stdlib/issues/2039)