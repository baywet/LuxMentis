
# Proof of Concept (POC): Task Automation with Semantic Kernel

## **DISCLAIMER:**
This project is not a recommended approach for building production-level task automation using Semantic Kernel. The setup used here is for **Proof of Concept (POC) purposes only** and should **not be seen as an endorsement** of the approach or as a demonstration of the art of the possible. The project makes several **simplifications** that would not hold up in a real-world, scalable application.

## Scenario

The goal of this project was to create a natural language-driven system that allows the user to summarize and organize tasks at the end of the day. Specifically, the user provides the following prompt:

```csharp
string prompt = $@"
Hey, I'm about to end my day and I know I haven't finished everything.
Let's set up the next day. For the people I work with the most, let's check to see if I have any important unread emails. 
Let's create a ToDo task for those and block some time in my calendar to address them.
";
```

### Approach Taken

We set up a series of **Semantic Kernel plugins** that can:
1. Check for important unread emails.
2. Create ToDo tasks based on the unread emails.
3. Block time in the user's calendar to complete the tasks the next day.

These tasks are driven by **natural language input** and processed automatically using the **auto-invoking kernel function** feature in Semantic Kernel. The key component that allows the automatic invocation of these functions is:

```csharp
OpenAIPromptExecutionSettings settings = new()
{
    ToolCallBehavior = ToolCallBehavior.AutoInvokeKernelFunctions
};
```

This feature allows the Semantic Kernel to automatically decide which plugins to invoke based on the natural language prompt.

## **Cheats and Limitations**

While the implementation successfully demonstrated how the **auto-invoking function feature** works, the approach includes **several significant cheats** that would not apply in a real-world scenario:

### **Cheat 1: Static Files as Data Stores**
We are using **static files** to represent the data store for emails, tasks, and calendar events (`email.txt`, `todo.txt`, `calendar.txt`). In a real-world scenario, these data sources would be **dynamic** and ever-changing, likely sourced from **real databases** or **APIs**.

### **Cheat 2: Fixed Set of People and Fields**
The plugins are working with a **fixed set of people** and fields hardcoded in the static data files. This setup is not flexible and doesn't reflect the nature of real-world interactions, where the people you interact with and the fields you need to reason over would constantly change.

### **Cheat 3: No Auth or Permissions Management**
This setup does not handle **authentication** or **permissions**. In a real-world application, the system would need to handle user authentication and ensure that data operations (such as accessing emails, tasks, or calendars) are appropriately permissioned.

## **Images of the Working POC**

Here are some screenshots of the **POC in action**, showing the tasks that were performed based on the prompt provided.

### Task Output in Terminal:
![Task Output](./images/FFE93165-80D6-496F-8D35-4D06B248C5A2.png)

### Code Structure:
![Code Structure](./images/EB39BB13-2EA9-4259-9A1B-AA4CF14E461A.png)

### Calendar and ToDo Files:
![Calendar and ToDo](./images/3C1B9589-0704-47A9-8A53-CDB06A9DC8E2.png)

### Summary of Actions:
![Summary of Actions](./images/C5E22CAE-BDDA-42A1-80A8-9D2C31673B10.png)

## Conclusion

This **Proof of Concept (POC)** demonstrates the ability to provide a **natural language-driven task automation system** using Semantic Kernel’s **auto-invoking kernel functions**. However, due to the limitations outlined above, this approach is **not suitable for production use**.

The focus of this POC was to illustrate the ease of plugging in natural language to manage different workflows without explicitly defining which functions are invoked.

In a real-world scenario, the approach would need to be adapted to handle dynamic data sources, authentication, and more flexible task management.