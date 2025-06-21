# **The Ultimate Guide to Building an Educational React Native Website on Agentic AI**

## **Part 1: Project Scaffolding and Setup**

This section provides a rock-solid foundation for the project, emphasizing best practices for scalability and maintainability within the Expo ecosystem. It walks through every step from environment setup to creating a clean, organized project structure ready for development.

### **Introduction: Why React Native for Web?**

React Native has long been celebrated for its ability to create cross-platform mobile applications from a single codebase. However, its capabilities extend beyond mobile. By leveraging frameworks like Expo, developers can use their existing React skills to build and deploy fully-featured websites. This "learn once, write anywhere" philosophy is incredibly powerful, allowing for the creation of a universal component library and business logic that can serve iOS, Android, and the web, drastically reducing development time and effort. This guide will harness that power to build a content-rich educational website.

### **Prerequisites: Gearing Up for Development**

Before beginning, it is essential to have the correct tools installed. A proper development environment is critical for a smooth workflow. The following tools are required:

* **Node.js and npm/yarn:** Node.js is the JavaScript runtime environment that executes JavaScript code outside of a web browser. It is the foundation of modern web development. It comes bundled with npm (Node Package Manager), a vast registry of software packages. Yarn is an alternative package manager that is also widely used. These tools are necessary for managing project dependencies and running development scripts.  
* **Git:** Git is the industry-standard distributed version control system. It is indispensable for tracking changes in the source code, collaborating with others, and managing different versions of the application. It will also be used to deploy the final website to GitHub Pages.  
* **A Code Editor (VS Code Recommended):** A capable code editor is where all development will take place. Visual Studio Code (VS Code) is highly recommended due to its excellent support for JavaScript/TypeScript, a rich ecosystem of extensions, and deep integration with tools like Git. For this project, extensions like ESLint (for code linting) and Prettier (for code formatting) are strongly advised to maintain code quality and consistency.

### **Choosing the Right Framework: The Case for Expo**

While it is possible to build a React Native application from scratch (a "bare" project), this guide strongly recommends using a framework. Frameworks provide a suite of tools and pre-configured libraries that handle common development challenges like navigation, native API access, and build processes, allowing developers to focus on building the application itself rather than the underlying infrastructure.  
For this project, **Expo** is the framework of choice. Expo offers a managed workflow that abstracts away much of the complexity of native development. Its key advantages include a rich library of universal APIs that work across platforms, over-the-air updates, and, most importantly for this guide, first-class support for web output. This makes it the ideal tool for creating a React Native for Web project quickly and efficiently.  
To initialize a new project, open a terminal and run the following command. This command creates a new Expo application named agentic-ai-site using the TypeScript template, which is a best practice for building robust and scalable applications.  
`npx create-expo-app@latest agentic-ai-site -t typescript`

### **Project Structure: A Blueprint for Scalability**

A well-organized folder structure is not a trivial matter; it is the architectural blueprint of a maintainable and scalable application. As a project grows, a logical structure prevents files from becoming disorganized, making it easier for developers to locate code, understand its purpose, and add new features without introducing chaos.  
The most critical architectural decision in a modern Expo project involves reconciling the "magic" of file-based routing with traditional, scalable React folder structures. A naive approach can lead to a messy app directory filled with business logic, while ignoring the router's conventions breaks the framework. The optimal structure, therefore, uses the app directory *only* as a routing and layout definition layer. Each file in app/ will be a lightweight "container" that imports its primary content from a corresponding file in a src/screens directory. This hybrid approach provides the best of both worlds: it leverages the power and simplicity of Expo Router for navigation while maintaining a clean, scalable, and logically separated codebase within src, which is crucial for long-term project health.  
The following structure is recommended for this project, synthesizing best practices for both Expo Router and large-scale React applications :  
`agentic-ai-site/`  
`├── app/             # Expo Router: All files here become routes.`  
`│   ├── (tabs)/      # A route group for the main layout.`  
`│   │   ├── _layout.tsx # Defines the shared layout (e.g., nav bar).`  
`│   │   ├── index.tsx     # Home page route.`  
`│   │   ├── basics.tsx    # Agentic AI Basics page route.`  
`│   │   ├── evolution.tsx # Agentic AI Evolution page route.`  
`│   │   ├── timeline.tsx  # LLM Timeline page route.`  
`│   │   └── ides.tsx      # Agentic AI IDEs page route.`  
`│   └── _layout.tsx    # Root layout for the entire app.`  
`├── assets/          # Static assets.`  
`│   ├── fonts/`  
`│   └── images/`  
`├── src/             # Main source code directory.`  
`│   ├── components/  # Reusable UI components (Cards, Buttons, etc.).`  
`│   │   ├── core/      # Basic, atomic components (Paragraph, Header).`  
`│   │   └── layout/    # Larger layout components (TimelineItem, Card).`  
`│   ├── navigation/  # Navigation-specific components (e.g., NavBar).`  
``│   ├── screens/     # UI and logic for each page, imported by `app/`.``  
`│   │   ├── HomeScreen.tsx`  
`│   │   ├── BasicsScreen.tsx`  
`│   │   └──...`  
`│   ├── styles/      # Global styles, theme, and constants.`  
`│   │   └── theme.ts`  
`│   └── types/       # TypeScript type definitions.`  
`│       └── index.ts`  
`├──.gitignore`  
`├── app.json`  
`├── package.json`  
`└── tsconfig.json`

### **GitHub Repository Setup**

With the local project created, the next step is to set up version control with Git and connect it to a remote repository on GitHub.

1. **Create a Repository on GitHub:** Navigate to GitHub.com and create a new, empty repository. Do not initialize it with a README or .gitignore file, as the local project already contains these.  
2. **Initialize and Link Local Project:** In the terminal, navigate to the root of the agentic-ai-site project directory and run the following commands. Replace your-username and your-repository-name with the actual GitHub username and repository name.

`# Navigate into your new project directory`  
`cd agentic-ai-site`

`# Initialize a new Git repository`  
`git init`

`# Stage all files for the initial commit`  
`git add.`

`# Create the first commit`  
`git commit -m "Initial commit: Setup Expo project with TypeScript"`

`# Add the remote repository URL`  
`git remote add origin https://github.com/your-username/your-repository-name.git`

`# Push the initial commit to the main branch on GitHub`  
`git push -u origin main`

The project is now set up, version-controlled, and ready for the implementation of its core features.

## **Part 2: Core Website Implementation**

This section focuses on building the skeleton of the application. It covers the setup of a multi-page navigation system and the creation of a library of reusable components. These components will serve as the fundamental building blocks for all the educational content pages.

### **Multi-Page Navigation with React Navigation**

Expo Router, the file-based routing solution used in this project, is built directly on top of the powerful React Navigation library. This means developers get the simplicity of file-based routing for defining pages while retaining access to the full suite of React Navigation's tools for creating complex navigation patterns like stacks, tabs, and drawers.  
First, install the necessary peer dependencies for React Navigation:  
`npx expo install react-native-screens react-native-safe-area-context`

With the dependencies installed, the main navigation structure can be created. For this website, a persistent top navigation bar is ideal. This will be implemented using a Tabs navigator within a route group. In the project structure, the (tabs) directory is a "layout group," meaning it doesn't add a segment to the URL but allows a shared layout file (\_layout.tsx) to be applied to all routes within it.  
Create the file app/(tabs)/\_layout.tsx and add the following code. This file defines the tab-based navigation bar.  
`// app/(tabs)/_layout.tsx`  
`import React from 'react';`  
`import { Tabs } from 'expo-router';`  
`import { Link } from 'expo-router';`  
`import { Pressable, useColorScheme } from 'react-native';`

`// A simple component to render the tab bar icons`  
`function TabBarIcon(props: { name: string; color: string }) {`  
  `// This is a placeholder. For a real app, you'd use an icon library.`  
  `return <span style={{ color: props.color, marginRight: 5 }}>●</span>;`  
`}`

`export default function TabLayout() {`  
  `const colorScheme = useColorScheme();`

  `return (`  
    `<Tabs`  
      `screenOptions={{`  
        `tabBarActiveTintColor: colorScheme === 'dark'? '#fff' : '#000',`  
        `headerShown: false, // We will handle headers inside each screen`  
      `}}>`  
      `<Tabs.Screen`  
        `name="index"`  
        `options={{`  
          `title: 'Home',`  
          `tabBarIcon: ({ color }) => <TabBarIcon name="home" color={color} />,`  
        `}}`  
      `/>`  
      `<Tabs.Screen`  
        `name="basics"`  
        `options={{`  
          `title: 'Agentic AI Basics',`  
          `tabBarIcon: ({ color }) => <TabBarIcon name="book" color={color} />,`  
        `}}`  
      `/>`  
      `<Tabs.Screen`  
        `name="evolution"`  
        `options={{`  
          `title: 'AI Evolution',`  
          `tabBarIcon: ({ color }) => <TabBarIcon name="trending-up" color={color} />,`  
        `}}`  
      `/>`  
      `<Tabs.Screen`  
        `name="timeline"`  
        `options={{`  
          `title: 'LLM Timeline',`  
          `tabBarIcon: ({ color }) => <TabBarIcon name="calendar" color={color} />,`  
        `}}`  
      `/>`  
      `<Tabs.Screen`  
        `name="ides"`  
        `options={{`  
          `title: 'AI IDEs',`  
          `tabBarIcon: ({ color }) => <TabBarIcon name="code" color={color} />,`  
        `}}`  
      `/>`  
    `</Tabs>`  
  `);`  
`}`

A critical aspect of web development is ensuring that navigation behaves as users expect, with proper URL handling in the browser's address bar and correct history management. Expo Router's \<Link\> component is essential here, as it renders a standard HTML \<a\> tag on the web, ensuring proper web navigation, search engine crawlability, and accessibility. The Tabs navigator from Expo Router automatically uses these links, providing a seamless web experience out of the box.

### **Creating Reusable Components: The DRY Principle in Action**

The "Don't Repeat Yourself" (DRY) principle is a cornerstone of efficient software development. By creating a set of reusable components, development is accelerated, a consistent look and feel is maintained across the application, and future updates become much easier to manage.  
The selection of components to create is not arbitrary; they are the semantic building blocks of the educational content. A Card is ideal for encapsulating discrete concepts, a TimelineItem is perfect for telling chronological stories, and Header and Paragraph components provide the basic document structure. This component-driven design enforces a consistent pedagogical structure across the entire site, enhancing the learning experience.  
The following components should be created within the src/components/ directory.

#### **Header.js**

This component provides a consistent, large-font header for each page title.  
*File: src/components/core/Header.tsx*  
`import React from 'react';`  
`import { Text, StyleSheet, View } from 'react-native';`

`interface HeaderProps {`  
  `title: string;`  
`}`

`export default function Header({ title }: HeaderProps) {`  
  `return (`  
    `<View style={styles.container}>`  
      `<Text style={styles.title}>{title}</Text>`  
    `</View>`  
  `);`  
`}`

`const styles = StyleSheet.create({`  
  `container: {`  
    `paddingVertical: 20,`  
    `borderBottomWidth: 1,`  
    `borderBottomColor: '#ddd',`  
    `marginBottom: 20,`  
  `},`  
  `title: {`  
    `fontSize: 32,`  
    `fontWeight: 'bold',`  
    `textAlign: 'center',`  
    `color: '#111',`  
  `},`  
`});`

#### **Paragraph.js**

This component standardizes the appearance of all body text.  
*File: src/components/core/Paragraph.tsx*  
`import React from 'react';`  
`import { Text, StyleSheet } from 'react-native';`

`interface ParagraphProps {`  
  `children: React.ReactNode;`  
`}`

`export default function Paragraph({ children }: ParagraphProps) {`  
  `return <Text style={styles.text}>{children}</Text>;`  
`}`

`const styles = StyleSheet.create({`  
  `text: {`  
    `fontSize: 16,`  
    `lineHeight: 24,`  
    `marginBottom: 16,`  
    `color: '#333',`  
  `},`  
`});`

#### **Card.js**

A versatile card component for displaying key concepts in a visually distinct way.  
*File: src/components/layout/Card.tsx*  
`import React from 'react';`  
`import { View, Text, StyleSheet } from 'react-native';`

`interface CardProps {`  
  `title: string;`  
  `children: React.ReactNode;`  
`}`

`export default function Card({ title, children }: CardProps) {`  
  `return (`  
    `<View style={styles.card}>`  
      `<Text style={styles.title}>{title}</Text>`  
      `<View>{children}</View>`  
    `</View>`  
  `);`  
`}`

`const styles = StyleSheet.create({`  
  `card: {`  
    `backgroundColor: '#fff',`  
    `borderRadius: 8,`  
    `padding: 20,`  
    `marginBottom: 20,`  
    `borderWidth: 1,`  
    `borderColor: '#eee',`  
    `// Shadow for web`  
    `shadowColor: '#000',`  
    `shadowOffset: { width: 0, height: 2 },`  
    `shadowOpacity: 0.1,`  
    `shadowRadius: 4,`  
    `elevation: 3, // for Android`  
  `},`  
  `title: {`  
    `fontSize: 20,`  
    `fontWeight: '600',`  
    `marginBottom: 10,`  
    `color: '#111',`  
  `},`  
`});`

#### **TimelineItem.js**

A specialized component for creating entries in a vertical timeline.  
*File: src/components/layout/TimelineItem.tsx*  
`import React from 'react';`  
`import { View, Text, StyleSheet } from 'react-native';`

`interface TimelineItemProps {`  
  `date: string;`  
  `title: string;`  
  `children: React.ReactNode;`  
`}`

`export default function TimelineItem({ date, title, children }: TimelineItemProps) {`  
  `return (`  
    `<View style={styles.container}>`  
      `<View style={styles.dateContainer}>`  
        `<Text style={styles.dateText}>{date}</Text>`  
      `</View>`  
      `<View style={styles.contentContainer}>`  
        `<Text style={styles.title}>{title}</Text>`  
        `<Text style={styles.description}>{children}</Text>`  
      `</View>`  
    `</View>`  
  `);`  
`}`

`const styles = StyleSheet.create({`  
  `container: {`  
    `flexDirection: 'row',`  
    `marginBottom: 30,`  
    `position: 'relative',`  
  `},`  
  `dateContainer: {`  
    `backgroundColor: '#007AFF',`  
    `borderRadius: 15,`  
    `paddingVertical: 5,`  
    `paddingHorizontal: 10,`  
    `alignSelf: 'flex-start',`  
  `},`  
  `dateText: {`  
    `color: '#fff',`  
    `fontWeight: 'bold',`  
    `fontSize: 14,`  
  `},`  
  `contentContainer: {`  
    `flex: 1,`  
    `marginLeft: 20,`  
    `paddingLeft: 20,`  
    `borderLeftWidth: 2,`  
    `borderLeftColor: '#007AFF',`  
  `},`  
  `title: {`  
    `fontSize: 18,`  
    `fontWeight: 'bold',`  
    `marginBottom: 5,`  
    `color: '#111',`  
  `},`  
  `description: {`  
    `fontSize: 16,`  
    `color: '#555',`  
    `lineHeight: 22,`  
  `},`  
`});`

With these core components and the navigation structure in place, the project is now ready for its educational content.

## **Part 3: Content for Each Page**

This section is the heart of the educational website. It populates the pages with well-researched, accurate content about Agentic AI, its evolution, the underlying Large Language Models (LLMs), and the tools used to build with them. Each page will utilize the reusable components created in Part 2 to ensure a clean, consistent, and effective presentation of information.

### **Page 1: Agentic AI Basics**

This page introduces the fundamental concepts of Agentic AI. The layout uses a main Header for the page title, followed by introductory Paragraphs and a series of Card components to break down each core idea into a digestible format.  
*Layout File: app/(tabs)/basics.tsx \-\> imports content from src/screens/BasicsScreen.tsx*

#### **Content for BasicsScreen.tsx:**

**What is an AI Agent?**  
An AI Agent is an autonomous system designed to perceive its environment, make decisions, and take actions to achieve specific goals without direct human intervention. Think of it as a digital entity with a purpose. Unlike traditional programs that follow a rigid set of instructions, an agent can respond dynamically to changing conditions. This field is closely related to agentic automation, where these systems are applied to manage and automate complex processes. The core principle is independence; the agent analyzes data, learns from it, and acts on its own to produce a result.  
**Core Components of an Agentic System**  
An agentic system is typically composed of four key components that work in a continuous loop:

* **Perception:** This is how the agent takes in information about its environment. This "environment" can be digital, like the internet, or physical, via sensors. Perception involves processing data from various sources, such as text from a user prompt, information from an API, visual data from an image, or readings from a sensor.  
* **Planning (or Reasoning):** This is the "brain" of the agent. Once it has perceived its environment and understood its goal, the agent must create a plan. This involves breaking down a large, complex goal into a series of smaller, manageable steps or sub-tasks. Modern agents often use a powerful LLM for this reasoning process, allowing them to understand nuanced instructions and devise sophisticated strategies.  
* **Action:** This component is how the agent interacts with and affects its environment. Actions are the execution of the steps defined in the planning phase. This could involve calling an external API, running a piece of code, sending an email, or controlling a robotic arm. The agent has a set of "tools" it can use to perform these actions.  
* **Memory:** For an agent to be effective, it needs memory. This includes short-term memory (or context) to keep track of the current task and recent actions, and long-term memory to learn from past experiences. By remembering what worked and what didn't, the agent can improve its performance over time, adapting its strategies and avoiding repeated mistakes.

**How is this Different from a Standard LLM?**  
It is crucial to distinguish between an AI agent and the LLM that often powers it. An LLM is a foundational component, but it is not an agent on its own. A simple analogy helps clarify the difference:  
An LLM is like an incredibly powerful, knowledgeable calculator. It can answer almost any question you ask and perform complex calculations in an instant. However, it only does what it's told, one step at a time. It won't decide which calculations are needed to solve a larger problem.  
An agentic AI system, on the other hand, is like the skilled engineer who uses that calculator. The engineer understands the overall goal (e.g., "design a bridge"), knows which formulas to use, in what order, and can interpret the results to make decisions. The agent uses the LLM (the calculator) as a tool to reason and plan, but it is the agent that orchestrates the entire process to achieve the final objective. In short, an LLM generates content; an agent executes tasks and achieves goals.

### **Page 2: Agentic AI Evolution (Post-GenAI)**

This page tells the story of how modern agentic AI came to be, tracing its roots from earlier concepts to the breakthroughs that made today's autonomous systems possible. The layout is a narrative flow using headers and paragraphs.  
*Layout File: app/(tabs)/evolution.tsx \-\> imports content from src/screens/EvolutionScreen.tsx*

#### **Content for EvolutionScreen.tsx:**

**The Pre-GenAI Era: Foundations of Autonomy**  
The dream of autonomous agents is not new. Its conceptual roots can be traced back to the mid-20th century with early work on machine intelligence and feedback systems. In the decades that followed, this led to the development of **expert systems**. These were rule-based AI programs designed to replicate the decision-making of a human expert in a narrow domain, like medical diagnosis or financial analysis. These systems had a "knowledge base" of facts and "if-then" rules, and an "inference engine" to reason through them. They were a crucial step, demonstrating that a machine could automate reasoning. However, they were brittle; their knowledge was manually coded, and they couldn't handle ambiguity or tasks outside their rigid rules. They had the structure of an agent but lacked a flexible, adaptive "brain."  
**The LLM Catalyst: A Brain for the Agent**  
The landscape changed dramatically with the advent of powerful, pre-trained generative AI, specifically large language models like GPT-3. These models, trained on vast swathes of the internet, provided the missing piece: a generalized reasoning and language understanding engine. For the first time, a system could understand complex, natural language instructions, reason about abstract concepts, and generate coherent plans without being explicitly programmed with rules for every situation. The LLM became the "brain" that could power a new generation of more flexible and capable agents.  
**Key Evolutionary Steps: Building the Modern Agent Stack**  
The journey from a powerful LLM to a functional agent involved several key conceptual breakthroughs that now form the basis of most agentic systems:

1. **From Zero-Shot Prompting to Chain-of-Thought (CoT):** Early interactions with LLMs were "zero-shot"—a user asked a question, and the model gave an answer. The breakthrough came with **Chain-of-Thought (CoT) prompting**. Researchers discovered that by simply instructing the model to "think step-by-step," its performance on complex reasoning tasks improved dramatically. The LLM would output its internal monologue, breaking a problem down into intermediate logical steps before arriving at a final answer. This was a pivotal moment, as it allowed the model to simulate a reasoning process, making its thinking more robust and transparent.  
2. **The ReAct Framework: Giving the Brain Hands:** While CoT gave the LLM the ability to "reason," it still couldn't interact with the outside world. The **ReAct framework**, introduced in 2023, solved this by synergizing reasoning and acting. ReAct established an iterative loop: **Thought \-\> Action \-\> Observation**. The agent uses the LLM to generate a *thought* (a reasoning step), which determines an *action* to take (e.g., search Google, query an API). The agent then executes that action using a "tool" and receives an *observation* (the result of the action). This observation feeds back into the next thought, allowing the agent to dynamically adjust its plan based on real-world information. ReAct effectively gave the reasoning brain a set of hands to interact with its environment.  
3. **The Emergence of Autonomous Agents: Auto-GPT and BabyAGI:** In early 2023, projects like **Auto-GPT** and **BabyAGI** went viral, capturing the public's imagination. These open-source projects took the concepts of LLM-driven planning and tool use and put them into a fully autonomous loop. A user would provide a high-level goal (e.g., "do market research on electric bikes"), and the agent would autonomously generate a task list, execute tasks (like browsing websites), save information to memory, and create new tasks based on the results, continuing until the goal was met. While these early systems were often inefficient and prone to getting stuck in loops, they provided a powerful proof-of-concept for what was possible, sparking a wave of research and development into autonomous AI agents.

### **Page 3: Background to LLM Evolutions: A Timeline View**

The rapid advancement of agentic AI is inextricably linked to the fierce competition and innovation in the underlying large language models. This timeline highlights the key model releases from 2023 through mid-2025 that have pushed the boundaries of what is possible. The layout uses a series of TimelineItem components to present this information chronologically.  
*Layout File: app/(tabs)/timeline.tsx \-\> imports content from src/screens/TimelineScreen.tsx*

#### **Content for TimelineScreen.tsx:**

The evolution from simple chatbots to complex AI agents has been driven by a series of groundbreaking LLM releases. Each new model or family of models introduced new capabilities or shifted the competitive landscape, creating a virtuous cycle of innovation. The following table details this progression.

| Model/Family | Approximate Release | Key Innovation / Impact |
| :---- | :---- | :---- |
| **GPT-4** | March 2023 | Set a new state-of-the-art for reasoning, multimodality, and factual accuracy. It became the gold standard for complex tasks and served as the primary engine for the first wave of agentic experiments like Auto-GPT. |
| **Gemini 1.0 Family** | December 2023 | Google's first major response to GPT-4, introducing a family of models (Pro, Ultra, Nano) designed from the ground up to be natively multimodal, processing text, images, and audio seamlessly. |
| **Claude 3 Family** | March 2024 | Anthropic's family of models (Haiku, Sonnet, Opus) established the company as a frontier competitor. The top-tier Opus model surpassed GPT-4 on several key industry benchmarks, particularly in complex reasoning and vision tasks. |
| **GPT-4o** | May 2024 | The "Omni" model represented a major shift in focus from raw intelligence to usability and efficiency. It offered GPT-4 level intelligence but with significantly faster speeds, lower cost, and natively integrated real-time voice and vision interaction, making advanced AI more accessible. |
| **Gemini 1.5 Pro & Flash** | Q1/Q2 2024 | Introduced a massive 1 million token context window, establishing a new competitive axis for LLMs. This allowed for the analysis of entire codebases, large documents, or hours of video in a single prompt, opening up new use cases. |
| **Claude 3.5 Sonnet** | June 2024 | A breakthrough release that dramatically raised the industry bar. Claude 3.5 Sonnet outperformed Anthropic's own top-tier Claude 3 Opus model in key areas like coding and reasoning, but at the speed and price of their mid-tier model, delivering frontier performance with unprecedented efficiency. |
| **Claude 3.7 Sonnet** | February 2025 | Introduced the concept of a "hybrid reasoning" model. It was optimized to respond instantly to simple queries while dedicating more computational "thought" to complex problems, allowing developers to trade speed for quality and improving overall agentic efficiency. |
| **Claude 4 (Opus & Sonnet)** | May 2025 | A new generation of models explicitly designed for AI agents. Claude 4 Opus was launched as the world's best coding model, demonstrating sustained performance on complex, long-running tasks and agentic workflows, setting a new frontier for what AI agents can accomplish. |
| **Gemini 2.5 Family** | Q2 2025 | Google's next evolution of models, branded as "thinking models" capable of enhanced reasoning. The family includes the highly capable 2.5 Pro and the fast, cost-effective 2.5 Flash and 2.5 Flash-Lite (released June 2025), designed for a wide range of production applications. |

This rapid succession of releases shows a clear trajectory. The industry first competed on raw intelligence (GPT-4 vs. Claude 3), then on new modalities like massive context windows (Gemini 1.5), and then on efficiency (GPT-4o, Claude 3.5). The latest frontier, as seen with Claude 4 and Gemini 2.5, is specialized optimization for reasoning and agentic workflows, indicating that the entire industry is now building towards a future of autonomous AI systems.

### **Page 4: Agentic AI IDEs & Tools: 2024 Onwards**

The evolution of LLMs has fueled a parallel evolution in developer tooling. We are moving from AI *assisting* with code to AI *writing* and *managing* code. This page surveys the landscape of modern AI-powered development tools, from integrated editors to fully autonomous agents. The layout uses a grid of Card components to profile each tool.  
*Layout File: app/(tabs)/ides.tsx \-\> imports content from src/screens/IdesScreen.tsx*

#### **Content for IdesScreen.tsx:**

As models have grown more capable, the tools built on them have become more ambitious. The developer's relationship with AI is shifting from that of a "mechanic" who writes every line of code to an "architect" who directs intelligent agents. This is reflected in the new class of agentic development tools.

* **Cursor:** An AI-first code editor. Cursor is a fork of VS Code that is deeply integrated with a GPT-4 level chat and code manipulation engine. Instead of a simple autocomplete, it allows developers to select blocks of code and provide natural language instructions for refactoring, debugging, or generation. It aims to make the entire editing experience conversational and AI-native.  
* **Codex (OpenAI):** The foundational model that started it all. While Codex itself is a model, not a tool, its integration into **GitHub Copilot** established the paradigm of AI code assistance. It was trained on billions of lines of code and demonstrated that an AI could translate natural language comments into functional code, paving the way for all subsequent tools.  
* **Claude Code:** Anthropic's tool for agentic coding. Often used in the terminal, Claude Code is designed to understand an entire codebase and perform complex, multi-file edits. It excels at tasks like turning a GitHub issue into a pull request, handling git workflows, and executing routine tasks through natural language commands, powered by the advanced coding capabilities of the Claude 4 models.  
* **Windsurf:** An advanced agentic code editor that takes context to the next level. Windsurf aims to understand the developer's intent across the entire project. It can automatically make changes, run the code, debug errors, and iterate on the solution until the requested task is successfully fulfilled, making the coding process more interactive and automated.  
* **Augment:** A platform designed to "augment" the developer's workflow. Augment indexes a project's entire codebase to provide a highly context-aware AI assistant. It can be used for understanding unfamiliar code, debugging complex issues, and guiding developers step-by-step through repetitive changes, effectively acting as an expert pair programmer that knows the project inside and out.  
* **The Next Wave (Jules, Cline, Roo):** These emerging tools represent the shift towards specialized, autonomous agents that handle high-level software engineering tasks.  
  * **Jules (Google):** An asynchronous coding agent. A developer gives Jules a high-level task (e.g., "fix this bug" or "add user authentication"), and Jules works on it in the background in a secure cloud environment. When finished, it presents a plan and a code diff for approval, acting like a junior developer on the team.  
  * **Cline:** An agent with deep architectural awareness. Cline is designed for large, complex, and multi-repository codebases. It excels at understanding the high-level design and dependencies of a system, making it suitable for architectural refactoring and ensuring consistency across microservices.  
  * **Roo:** A highly customizable agent that can adopt different "personas." A developer can configure Roo to act as a "QA engineer" to write tests, a "security auditor" to find vulnerabilities, or a "product manager" to help with documentation. This flexibility allows it to assist with multiple roles within the software development lifecycle.

## **Part 4: Deployment to GitHub Pages**

This final section provides a clear, actionable checklist to take the project from a local development environment to a live, publicly accessible website hosted for free on GitHub Pages.

### **Preparing for Deployment**

The first step in deploying a web application is to create a static build. This process compiles all the TypeScript, JSX, and other assets into plain HTML, CSS, and JavaScript files. These static files can then be served by any standard web server, including GitHub Pages.

### **Building the Web App**

Expo provides a single command to generate this static build. This command bundles the application for the web platform and places the output in a dist directory at the root of the project.  
Run the following command in the terminal:  
`npx expo export -p web`

After the command completes, a new dist folder will be present in the project directory. This folder contains the entire static website.

### **Configuring for GitHub Pages**

To automate the deployment process, the gh-pages package is used. This utility simplifies the process of pushing the contents of the dist folder to a special branch in the GitHub repository that GitHub Pages uses for hosting.

1. **Install gh-pages:** Install the package as a development dependency.  
   `npm install gh-pages --save-dev`

2. **Configure package.json:** Two modifications are needed in the package.json file.  
   * First, add a homepage property. This tells the build process the final URL where the site will be hosted. This is crucial for ensuring that asset paths are generated correctly. Replace your-username and your-repository-name.  
   * Second, add two scripts: predeploy and deploy. The predeploy script will automatically run the build command before every deployment. The deploy script will use the gh-pages package to push the dist folder to the gh-pages branch on GitHub. The \--nojekyll flag is important as it prevents GitHub Pages from ignoring files that begin with an underscore, which Expo generates.

*File: package.json*`{`  
  `"name": "agentic-ai-site",`  
  `"version": "1.0.0",`  
  `"main": "expo-router/entry",`  
  `"homepage": "https://your-username.github.io/your-repository-name",`  
  `"scripts": {`  
    `"start": "expo start",`  
    `"android": "expo start --android",`  
    `"ios": "expo start --ios",`  
    `"web": "expo start --web",`  
    `"predeploy": "npx expo export -p web",`  
    `"deploy": "gh-pages -d dist --nojekyll"`  
  `},`  
  `"dependencies": {`  
   `...`  
  `},`  
  `"devDependencies": {`  
    `"gh-pages": "^6.1.1",`  
   `...`  
  `},`  
  `"private": true`  
`}`

### **The Final Deployment**

With the configuration complete, the deployment is now a single command.

1. **Commit and Push Changes:** Make sure all code changes, especially the updates to package.json, are committed to Git and pushed to the main branch on GitHub.  
   `git add.`  
   `git commit -m "Configure for GitHub Pages deployment"`  
   `git push origin main`

2. **Run the Deploy Script:** Execute the deploy script from the terminal.  
   `npm run deploy`  
   This command will first run predeploy (building the site into the dist folder) and then run deploy (pushing the contents of dist to the gh-pages branch of the remote repository).  
3. **Configure GitHub Repository Settings:** The final step is to tell GitHub to serve the website from the newly created gh-pages branch.  
   * Navigate to the GitHub repository on the web.  
   * Go to the **Settings** tab.  
   * In the left sidebar, click on **Pages**.  
   * Under "Build and deployment," change the **Source** to **Deploy from a branch**.  
   * Under "Branch," select gh-pages as the source branch and / (root) as the folder.  
   * Click **Save**.

GitHub will now publish the site. After a minute or two, the educational website on Agentic AI will be live at the URL specified in the homepage property of the package.json file.

#### **Works cited**

1\. Get Started with React Native · React Native, https://reactnative.dev/docs/environment-setup 2\. 12 tips for setting up your next Expo project, https://expo.dev/blog/12-tips-for-setting-up-your-next-expo-project 3\. The Ultimate Guide to the Best Folder Structure in React Native ..., https://dev.to/ersuman/the-ultimate-guide-to-the-best-folder-structure-in-react-native-dc4 4\. Project Structure | React Native / Expo Starter \- Obytes Starter, https://starter.obytes.com/getting-started/project-structure/ 5\. Boost the structuring of React Native Projects with Testim ... \- Tricentis, https://www.tricentis.com/learn/react-native-project-structure 6\. What's the Recommended Architecture for a React Native (Expo) Project? \- Reddit, https://www.reddit.com/r/expo/comments/1i6r5r9/whats\_the\_recommended\_architecture\_for\_a\_react/ 7\. Publish websites \- Expo Documentation, https://docs.expo.dev/guides/publishing-websites/ 8\. Getting started | React Navigation, https://reactnavigation.org/docs/getting-started/ 9\. Agentic AI \- Wikipedia, https://en.wikipedia.org/wiki/Agentic\_AI 10\. www.ibm.com, https://www.ibm.com/think/topics/components-of-ai-agents\#:\~:text=Some%20key%20components%20are%20sequencing,coordinate%20or%20negotiate%20for%20resources. 11\. What is a ReAct Agent? | IBM, https://www.ibm.com/think/topics/react-agent 12\. LLMs, AI Agents, and Agentic AI: Understanding the Next AI ..., https://ili.digital/resource/understanding-llms-ai-agents-agentic-ai/\#:\~:text=LLMs%20are%20powerful%20for%20generating,%2C%20plan%2C%20and%20act%20independently 13\. ili.digital, https://ili.digital/resource/understanding-llms-ai-agents-agentic-ai/\#:\~:text=LLMs%20are%20powerful%20for%20generating,%2C%20plan%2C%20and%20act%20independently. 14\. Expert Systems in AI \- GeeksforGeeks, https://www.geeksforgeeks.org/artificial-intelligence/expert-systems/ 15\. Chain of Thought Prompting \- .NET \- Learn Microsoft, https://learn.microsoft.com/en-us/dotnet/ai/conceptual/chain-of-thought-prompting 16\. What is chain of thought (CoT) prompting? | IBM, https://www.ibm.com/think/topics/chain-of-thoughts 17\. AutoGPT vs BabyAGI: An In-depth Comparison \- SmythOS, https://smythos.com/developers/agent-comparisons/autogpt-vs-babyagi/ 18\. BabyAGI Complete Guide: What It Is and How Does It Work? \- AutoGPT, https://autogpt.net/babyagi-complete-guide-what-it-is-and-how-does-it-work/ 19\. Cursor (code editor) \- Wikipedia, https://en.wikipedia.org/wiki/Cursor\_(code\_editor) 20\. Cursor \- The AI Code Editor, https://www.cursor.com/ 21\. RooCodeInc/Roo-Code: Roo Code (prev. Roo Cline) gives ... \- GitHub, https://github.com/RooCodeInc/Roo-Code 22\. OpenAI Codex \- Wikipedia, https://en.wikipedia.org/wiki/OpenAI\_Codex 23\. anthropics/claude-code: Claude Code is an agentic coding tool that lives in your terminal, understands your codebase, and helps you code faster by executing routine tasks, explaining complex code, and handling git workflows \- all through natural language commands. \- GitHub, https://github.com/anthropics/claude-code 24\. Claude Code: Deep Coding at Terminal Velocity \\ Anthropic, https://www.anthropic.com/claude-code 25\. Windsurf AI Agentic Code Editor: Features, Setup, and Use Cases ..., https://www.datacamp.com/tutorial/windsurf-ai-agentic-code-editor 26\. Introduction \- Augment, https://docs.augmentcode.com/introduction 27\. Meet Augment: The AI Dev Tool That Codes Like You Think \- Analytics Vidhya, https://www.analyticsvidhya.com/blog/2025/05/augment-ai/ 28\. Jules: Google's autonomous AI coding agent \- Google Blog, https://blog.google/technology/google-labs/jules/ 29\. Cline vs Cursor: Which AI Coding Tool Is Better? \[2025\] \- Qodo, https://www.qodo.ai/blog/cline-vs-cursor/ 30\. Discover Cline: The Next-Generation AI Coding Tool \- Apidog, https://apidog.com/blog/what-is-cline/