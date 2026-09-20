� Level 1 — Core Foundation
These are the concepts you should understand very clearly.
1. What is Ansible? — Conguration management, automation and orchestration
2. Why Ansible? — What problem it solves in real infrastructure
3. Ansible Architecture — Controller → SSH → Managed Nodes
4. Agentless Architecture — Why agents aren't required
5. Inventory — How Ansible knows which servers to manage
. Static Inventory
7. Dynamic Inventory
. Groups & Child Groups
9. Variables — How data is passed to automation
10. Facts — Information Ansible gathers about servers
11. Ad-hoc Commands — Quick one-time automation
12. Modules — The actual units that perform work
🟢 Level 2 — Playbooks
This is the heart of Ansible.
13. YAML basics for Ansible
14. Playbook
Exported with AI Exporter 1 / 9
1
5. P
l
a
y
1
. Ta
s
k
1
7. M
o
d
u
l
e
+
A
r
g
u
m
e
n
t
s
1
. N
a
m
e
1
9. B
e
c
o
m
e
/
P
r
i
v
i
l
e
g
e Es
c
a
l
a
t
i
o
n
2
0. H
a
n
d
l
e
r
s
2
1. N
o
t
i
f
y
2
2. Ta
g
s
2
3. C
h
e
c
k
M
o
d
e
(
-
-
c
h
e
c
k
)
2
4. D
i
f
f
M
o
d
e
(
-
-
d
i
f
f
)
2
5. I
d
e
mpo
t
e
n
c
y
T
hin
k: 🟡 Le
v
el 3
—
V
a
r
i
a
ble
s
&
D
a
t
a
V
e
ry im
p
o
rt
a
n
t
f
o
r
r
e
al p
r
o
j
e
c
t
s. 2. Variable denition 27. Variable precedence 2. Host variables 29. Group variables 30. Command-line variables (
-
e
)
3
1. R
e
g
i
s
t
e
r
e
d
v
a
r
i
abl
e
s
3
2. F
a
c
t
s
3
3. M
a
g
i
c
v
a
r
i
abl
e
s
3
4. J
i
n
j
a
2
t
e
mpl
a
t
i
n
g
text Play
b
o
o
k
↓
P
l
a
y↓
T
a
s
k
s
↓
M
o
d
u
l
e
s
↓
M
a
n
a
g
e
d
S
e
r
v
e
r
E
x
p
o
rt
e
d
wit
h
AI E
x
p
o
rt
e
r
2
/
9
35. Conditions ( when )
3. Loops
37. Loop variables
3. Filters
The important mental model:
🟡 Level 4 — Conguration & Application Deployment
39. Package management
40. Service management
41. User management
42. File & directory management
43. File permissions / ownership
44. Copy module
45. Template module
4. Lineinle
47. Blockinle
4. Command vs Shell
49. Git module
50. Archive / Unarchive
51. Cron jobs
These are the modules you'll repeatedly encounter in DevOps work.
🟡 Level 5 — Templates
52. Jinja2
53. Variables inside templates
54. Conditions inside templates
text
Variables
↓
Jinja2
↓
Dynamic Playbook
Exported with AI Exporter 3 / 9
55. Loops inside templates
5. Template les ( .j2 )
57. Dynamic conguration generation
Example:
🟠 Level 6 — Roles
This is where Ansible starts becoming production-style.
5. Why Roles?
59. Role structure
0. tasks/
1. handlers/
2. templates/
3. les/
4. vars/
5. defaults/
. meta/
7. Role dependencies
. Using roles in playbooks
Mental model:
text
Ansible variables
↓
Jinja2
↓
nginx.conf.j2
↓
/etc/nginx/nginx.conf
text
Role
├── tasks
├── handlers
├── templates
├── files
├── vars
├── defaults
Exported with AI Exporter 4 / 9
🟠 Level 7 — Ansible Galaxy & Collections
9. Ansible Galaxy
70. Installing roles
71. Collections
72. Installing collections
73. Using community modules
74. FQCN
75. Requirements les
Example:
🟠 Level 8 — Secrets & Security
7. Ansible Vault
77. Encrypting secrets
7. Vault passwords
79. Vault IDs
0. Secrets in variables
1. SSH keys
2. Become passwords
3. Avoiding secrets in Git
Important real-world ow:
└── meta
yaml
community.general
ansible.posix
amazon.aws
kubernetes.core
text
Git
↓
Ansible Playbook
↓
Exported with AI Exporter 5 / 9
🔴 Level 9 — Advanced Ansible
You don't need to spend huge amounts of time here initially.
4. Blocks
5. Rescue
. Always
7. Error handling
. Delegation
9. delegate_to
90. run_once
91. Local actions
92. Serial execution
93. Rolling deployments
94. Async tasks
95. Retries / Until
9. Wait for
97. Conditionals
9. Complex loops
99. Custom modules
100. Ansible conguration ( ansible.cfg )
🔴 Level 10 — Production / DevOps Integration
These are useful when connecting Ansible with your other DevOps knowledge.
101. Ansible + AWS
102. Dynamic AWS inventory
103. Ansible + Terraform
104. Ansible + Jenkins
105. Ansible in CI/CD
Ansible Vault
↓
Secret
↓
Server
Exported with AI Exporter 6 / 9
10. Ansible + Docker
107. Ansible + Kubernetes
10. Conguration drift
109. Rolling deployment
110. Zero/minimal-downtime deployment
111. Environment management — dev/stage/prod
112. Ansible project structure
113. Logging & troubleshooting
114. Ansible linting
115. Testing Ansible
