Security by Design
Security should not be an afterthought or add-on. When developing systems, you should begin with identifying relevant security requirements and treat them as an integral part of the overall process and system design. Commit to secure operations by developing secure "operational management" principles and practices.

Security by Default
Default configuration settings ensure a reasonable level of security. Evaluate what the settings should be, based on both risk analysis and usability tests. Configure the system to only provide the least functionality and to specifically prohibit and/or restrict the use of all other functions, ports, protocols, and/or services. Also configure the defaults to be as restrictive as possible, according to best practices, without compromising the "Psychological acceptability" and "Usability and Manageability" of the system.

Defense in Depth
Defense in depth is a security principle where defense against attack is provided by multiple security controls. The aim is that single points of complete compromise are eliminated or mitigated by the incorporation of a series or multiple layers of security safeguards and risk-mitigation countermeasures. If one layer of defense turns out to be inadequate then, if diverse defensive strategies are in place, another layer of defense may prevent a full breach and if that one is circumvented then the next layer may block the exploit.

Fail Safe
This is a security principle that aims to maintain confidentiality, integrity and availability when an error condition is detected. These error conditions may be a result of an attack, or may be due to design or implementation failures, in any case the system / applications should default to a secure state rather than an unsafe state.

For example unless an entity is given explicit access to an object, it should be denied access to that object by default. This is often described as 'Fail Safe Defaults' or 'Secure by Default'.

Least Privilege
A security principle in which a person or process is given only the minimum level of access rights (privileges) that is necessary for that person or process to complete an assigned operation. This right must be given only for a minimum amount of time that is necessary to complete the operation.

Compartmentalize
The principle of least privilege works better if access rights are not an "all or nothing" access model. Instead, compartmentalize the access to information on a "need-to-know" basis in order to perform certain tasks. The compartmentalization principle helps in minimizing the impact of a security breach in case of a successful breach attempt but must be used in moderation in order to prevent the system from becoming unmanageable. 

Separation of Duties
Separation of duties is a security principle which requires that the successful completion of a single task is dependent upon two or more conditions that are insufficient, individually by themselves, for completing the task.

Keep it Simple
If there are multiple implementations then the simplest and most easily understood implementation should be chosen.

Complete Mediation
A security principle that ensures that authority is not circumvented in subsequent requests of an object by a subject, by checking for authorization (rights and privileges) upon every request for the object.

Least Common Mechanism
The security principle of least common mechanisms disallows the sharing of mechanisms that are common to more than one user or process if the users or processes are at different levels of privilege. This is important when defending against privilege escalation.

Usability and Manageability
The configuration, administration and integration of security components should not be overly complex or obscure. Therefore, always use open standards for portability and interoperability, use common language in developing security requirements, design security to allow for regular adoption of new technology, ensure a secure and logical upgrade process exist, automate security management activities and strive for operational ease of use.

Secure the Weakest Link
This security principle states that the resiliency of your software against hacker attempts will depend heavily on the protection of its weakest components, be it the code, service or an interface. Therefore, identifying the weakest component and addressing the most serious risk first, until an acceptable level of risk is attained, is considered good security practice.