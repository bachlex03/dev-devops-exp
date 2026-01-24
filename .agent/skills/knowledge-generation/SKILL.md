---
name: knowledge-generation
description: A skill to generate comprehensive documentation and knowledge base items using the 5W1H framework in a bilingual format (English and Vietnamese).
---

# Knowledge Generation Skill

This skill allows the agent to systematically generate documentation and knowledge entries. It ensures that all information is complete, structured, and accessible to both English and Vietnamese speakers.

## Core Strategy: 5W1H (Flexible)

Every knowledge entry should aim to address the following questions, but **flexibility is encouraged**. If a specific factor (like "Who" or "When") is not relevant to the technical topic, it should be omitted to keep the content focused.

1.  **What**: Define the concept, tool, or topic.
2.  **Who**: Identify creators, maintainers, or audience (Optional - omit if not relevant).
3.  **Where**: Specify environment, location, or context.
4.  **When**: Define timing, lifecycle, or scenarios.
5.  **Why**: Explain purpose, benefits, or problems solved.
6.  **How**: Describe implementation, workflow, or mechanism.

## Language Requirement

Documentation must be provided in two languages:
-   **English (en)**
-   **Vietnamese (vi)**

## Output Format

The output should follow this structure (adaptable based on which 5W1H elements are used):

```markdown
## [Topic Name]

- **en**:
    - **What**: ...
    - **Where**: ...
    - **Why**: ...
    - **How**: ...

- **vi**:
    - **What (Cái gì)**: ...
    - **Where (Ở đâu)**: ...
    - **Why (Tại sao)**: ...
    - **How (Như thế nào)**: ...
```

## Usage Guidelines

-   **Be Concise**: Use bullet points for readability.
-   **Technical Accuracy**: Ensure terms are translated correctly or kept in English if they are industry standards.
-   **Consistency**: Maintain a professional tone in both languages.
-   **Flexibility First**: Do not force all 5W1H elements if they don't add value. For example, for internal components, "Who" is often unnecessary.

## Example (Flexible 5W1H)

### Topic: Kubernetes Pod

- **en**:
    - **What**: The smallest deployable unit in Kubernetes, representing a single instance of a running process.
    - **Where**: Runs on a Node within a Kubernetes cluster.
    - **When**: Created when you deploy an application; usually managed by a Deployment or ReplicaSet.
    - **Why**: To provide an execution environment for containers with shared network and storage resources.
    - **How**: Pods are defined in YAML and scheduled onto nodes by the kube-scheduler.

- **vi**:
    - **What (Cái gì)**: Đơn vị nhỏ nhất có thể triển khai trong Kubernetes, đại diện cho một instance duy nhất của một tiến trình đang chạy.
    - **Where (Ở đâu)**: Chạy trên một Node trong cụm Kubernetes.
    - **When (Khi nào)**: Được tạo khi bạn triển khai ứng dụng; thường được quản lý bởi Deployment hoặc ReplicaSet.
    - **Why (Tại sao)**: Cung cấp môi trường thực thi cho các container với tài nguyên mạng và lưu trữ dùng chung.
    - **How (Như thế nào)**: Pod được định nghĩa bằng YAML và được lập lịch lên các node bởi kube-scheduler.
