# Using SGX in SpacePanda

## TEE

**Trusted Execution Environment (TEE)** is a concept that extends the instruction set of a processor to allow for programs to run in a separate secure environment. The separation between this secure environment and the ones we are used to deal with already (often called “rich” execution environment) is done via hardware. So what ends up happening is that modern CPUs run both a normal OS as well as a secure OS simultaneously. Both have their own set of registers but share most of the rest of the CPU architecture (and of course system). By using clever CPU-enforced logic, data from the secure world cannot be accessed from the normal world.

TEE like all other hardware solutions has been a concept developed independently by different vendors, and then a standard trying to play catch up (by Global Platform). The most known TEEs are Intel’s **Software Guard Extensions (SGX)** and ARM’s **TrustZone**. But there are many more like AMD PSP, RISC-V MultiZone and IBM Secure Service Container. Here we mainly use **SGX** for SpacePanda generation.

## **Intel Software Guard Extensions**

[Intel Software Guard Extensions](https://software.intel.com/content/www/us/en/develop/topics/software-guard-extensions.html) (SGX) is a security instruction set baked into many of Intel’s x86-based central processing units (CPUs). SGX gives developers the ability to split a computer’s memory into what are called enclaves, which are private, predefined areas in memory that can better protect users’ sensitive information.

Put a different way, SGX encrypts sections of memory using security instructions native to the CPU. It’s a form of hardware-based encryption that allows users to protect their most-sensitive data by placing it into a highly secured environment within memory.

![A brief explanation of how Intel SGX protects your data. ](<../.gitbook/assets/intel sgx tutorial.webp>)

## **SpacePanda Trusted Generator**

[Rust SGX SDK](https://github.com/apache/incubator-teaclave-sgx-sdk) is used to generate SpacePanda with Intel SGX  in Rust programming language. All the generation logic can be found in our Github project [trusted-seed-generator](https://github.com/Space-Pandas/trusted-seed-generator).
