# Generative Software, Proof of Concept

**A self-evolving console application that dynamically extends its capabilities through AI-generated modules**

## Overview
This experimental console application demonstrates a novel approach to software development where the application can generate, compile, and integrate new features at runtime based on natural language descriptions. Leveraging both local and cloud-based LLMs, the system creates C# modules that implement features to satify the input request, automatically generate documentation, manages version control through GitHub integration, and maintains audit trails of all development activities. The generated modules can also run as independent applications.

## Key Features
- **AI-Powered Module Generation**  
  Create new features using natural language through online or local LLM models
- **Multi-Model Architecture**  
  Supports both online (DeepSeek V3 and R1) and offline (Ollama with available models) LLM options
- **Dynamic Compilation**  
  Automatic Roslyn-based compilation of generated code into working DLL modules
- **GitHub Integration**  
  Automatic version control and synchronization with GitHub repositories
- **Self-Healing Capability**  
  Automatic error diagnosis and code correction through iterative LLM prompting
- **Self-Upgrading Capability**
  Proactive identification of potential enhancements, optimizations, or new feature opportunities through continuous system analysis and LLM evaluation. Automatically suggests improvements and implements approved changes through the module generation pipeline.
- **Self-Documenting Capability** A contunue self analisys allows the system to automatically document the implemented features and any other change in the source code.
- **Audit System**  
  Detailed logging of all LLM interactions and compilation attempts
- **Version Management**  
  Automatic semantic versioning and historical tracking of module iterations

## Installation
### Prerequisites
- .NET 9 SDK
- Ollama (for local model usage)
- DeepSeek API key (for cloud model)
- [GitHub Personal Access Token ](https://github.com/settings/tokens)

### Download compiled version
- [SelfEvolvingSoftware_PoC_1_0-linux-x64](https://github.com/dancasmed/SelfEvolvingSoftware-public/releases/download/v1.0.0/SelfEvolvingSoftware_PoC_1_0-linux-x64.zip)
- [SelfEvolvingSoftware_PoC_1_0-osx-arm64](https://github.com/dancasmed/SelfEvolvingSoftware-public/releases/download/v1.0.0/SelfEvolvingSoftware_PoC_1_0-osx-arm64.zip)
- [SelfEvolvingSoftware_PoC_1_0-win-x64](https://github.com/dancasmed/SelfEvolvingSoftware-public/releases/download/v1.0.0/SelfEvolvingSoftware_PoC_1_0-win-x64.zip)

## Configuration

1. Configure model and GitHub preferences in config.json:
```json
  {
    "UseOnlineLLM": true,
    "UseOfflineLLM": true,
    "UseGitHub": true,
    "DeepSeekAPIKey": "DEEPSEEK_API_KEY",
    "DeepSeekAPIUrl": "https://api.deepseek.com/chat/completions",
    "OnlineReasoningModel": "deepseek-reasoner",
    "OnlineModel": "deepseek-chat",
    "OllamaUrl": "http://127.0.0.1:11434/api/chat",
    "OfflineModel": "llama3.3:70b-instruct-q8_0",
    "OfflineReasonModel": "deepseek-r1:70b",
    "GitHubToken": "GITHUB_API_KEY",
    "GitHubUser": "GITHUB_USER",
    "GitHubRepository": "GITHUB_REPOSITORY"
  }
```

2. Install required Ollama models:
```bash
ollama pull llama3.3:70b-instruct-q8_0

or 

ollama pull deepseek-r1:70b
```

## Usage
```bash
./PoC_1
```

### Main Menu Options:

1. **Create new module** - Creates a new module
2. **List working modules** - List all the modules with a valid compilation
3. **Load existing module** - Load and execute an existing module
4. **Upgrade module** - Upgrade an existing module with adding a new feature
5. **List modules with errors** - List all the modules with errors
6. **Recompile module with errors** - Recompile the source code of an existing module
7. **Delete module** - Deletes an existing module
8. **Process creation batch** - Reads a file with multiple module descriptions to create each module
9. **Generate stats** - Generate statistics based in all audit data
10. **Exit** - Ends the execution of the application

The system automatically:

- Synchronizes with configured GitHub repository on startup
- Maintains module versions in workspace/<module>/versions
- Stores audit logs in workspace/<module>/audit
- Generate updated documentation based in the implemented source code

## Generated module folder Structure
```
workspace/
├── <Module Name>/
│   ├── src/          # Generated source code
│   ├── bin/          # Compiled DLLs
│   ├── data/         # Module-specific data storage
│   ├── audit/        # LLM interaction logs and error reports
│   └── versions/     # Historical versions of the module
```

## Security Considerations

- Model Safety: Local model usage recommended for sensitive module features
- Code Validation: All generated code undergoes compilation checks
- Data Isolation: Module data stored in separate JSON files

## Example Prompts

- *"Need help to manage my vinyl record collection"*

- *"im a teacher, have multiple groups and need help to manage the daily assistance list for each group. At the end of the week I need a summary for the percentage os assitance per group"*

- *"Create an application that analyzes email messages (.eml) and suggests responses using NLP. Requiremenets: - Integrate Azure Cognitive Services for text analysis. - Recognize intent (claim, inquiry, purchase) and generate base responses. - Interface to edit responses before saving. - Response time statistics (using Stopwatch)."*

## Dependencies

- [Roslyn Compiler](https://github.com/dotnet/roslyn)
- [Octokit](https://github.com/octokit/octokit.net)
- [LibGit2Sharp](https://github.com/libgit2/libgit2sharp)

## Contributing

This proof of concept welcomes:

- Bug reports via GitHub Issues
- Security vulnerability disclosures
- Documentation improvements
- Experimental feature branches

## Disclaimer

This is experimental software. Use at your own risk. Generated code should be thoroughly reviewed before deployment in production environments.