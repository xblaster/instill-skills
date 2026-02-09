# Instill Skills Repository

A curated collection of coding standards, architectural patterns, and best practices for use with [Instill](https://github.com/xblaster/instill).

## 📚 Available Skills

This repository contains the following skills:

- **typescript-best-practices.md** - TypeScript coding standards and patterns
- **react-patterns.md** - React component patterns and hooks best practices
- **security-audit.md** - Security checklist for applications

## 🚀 Usage

To use these skills in your Instill project:

1. Add this repository as a remote source:
   ```bash
   instill sources
   ```
   Then select "Add Remote Source" and enter:
   ```
   https://github.com/YOUR_USERNAME/instill-skills
   ```

2. Run Instill and select the skills you want to use:
   ```bash
   instill init
   ```

3. Choose which AI assistants to apply them to:
   - Claude Code
   - Cursor
   - VS Code
   - Gemini
   - Others

## 📝 Structure

```
instill-skills/
├── skills/
│   ├── typescript-best-practices.md
│   ├── react-patterns.md
│   └── security-audit.md
├── README.md
└── LICENSE
```

Each skill is a standalone Markdown file that can be applied to different IDE integrations.

## 🤝 Contributing

Contributions are welcome! To add new skills:

1. Create a new Markdown file in the `skills/` directory
2. Follow the existing format and structure
3. Test with your local Instill installation
4. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🔗 Related

- [Instill GitHub Repository](https://github.com/xblaster/instill)
- [Instill Documentation](https://github.com/xblaster/instill#readme)

---

Built as part of the Instill ecosystem for managing AI assistant context.
