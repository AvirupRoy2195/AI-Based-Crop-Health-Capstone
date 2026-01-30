# Contributing to AI-Based Crop Health Monitoring

Thank you for your interest in contributing to this project! We welcome contributions from the community to help improve and extend this precision agriculture solution.

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Development Setup](#development-setup)
- [Pull Request Process](#pull-request-process)
- [Style Guidelines](#style-guidelines)
- [Reporting Bugs](#reporting-bugs)
- [Suggesting Enhancements](#suggesting-enhancements)

---

## Code of Conduct

This project adheres to a Code of Conduct that all contributors are expected to follow. Please be respectful and inclusive in all interactions.

### Our Standards

- **Be Respectful**: Treat everyone with respect and kindness
- **Be Inclusive**: Welcome people of all backgrounds and experience levels
- **Be Collaborative**: Work together to create the best possible solutions
- **Be Constructive**: Provide helpful feedback and accept criticism gracefully

---

## How Can I Contribute?

### 🐛 Reporting Bugs

If you find a bug, please open an issue with:

1. **Clear title** describing the bug
2. **Steps to reproduce** the issue
3. **Expected behavior** vs **actual behavior**
4. **Environment details** (Python version, OS, package versions)
5. **Screenshots** if applicable

### 💡 Suggesting Enhancements

Have an idea for improvement? Open an issue with:

1. **Clear description** of the enhancement
2. **Use case** explaining why this would be useful
3. **Proposed implementation** (optional)
4. **Alternatives considered** (optional)

### 📝 Documentation

Help improve our documentation by:

- Fixing typos or unclear explanations
- Adding examples or tutorials
- Translating documentation
- Improving code comments

### 💻 Code Contributions

We welcome code contributions for:

- Bug fixes
- New features
- Performance improvements
- Test coverage improvements
- Refactoring

---

## Development Setup

### Prerequisites

- Python 3.10 or higher
- Git
- Jupyter Notebook or JupyterLab

### Setup Steps

1. **Fork the repository**

   ```bash
   # Click "Fork" on GitHub
   ```

2. **Clone your fork**

   ```bash
   git clone https://github.com/YOUR_USERNAME/AI-Based-Crop-Health-Capstone.git
   cd AI-Based-Crop-Health-Capstone
   ```

3. **Create a virtual environment**

   ```bash
   python -m venv venv
   # Windows
   venv\Scripts\activate
   # Linux/Mac
   source venv/bin/activate
   ```

4. **Install dependencies**

   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn shap lime statsmodels scipy openpyxl
   ```

5. **Create a branch for your work**

   ```bash
   git checkout -b feature/your-feature-name
   ```

---

## Pull Request Process

1. **Ensure your code works**
   - Run the entire notebook without errors
   - Test any new functionality

2. **Update documentation**
   - Update README.md if needed
   - Add docstrings to new functions
   - Update METHODOLOGY.md for significant changes

3. **Follow style guidelines**
   - See [Style Guidelines](#style-guidelines) below

4. **Create the Pull Request**
   - Provide a clear title and description
   - Reference any related issues
   - Include screenshots for UI changes

5. **Respond to review feedback**
   - Address reviewer comments
   - Make requested changes promptly

### PR Checklist

- [ ] Code runs without errors
- [ ] Documentation updated
- [ ] Style guidelines followed
- [ ] Commits have meaningful messages
- [ ] No sensitive data included

---

## Style Guidelines

### Python Code Style

Follow [PEP 8](https://www.python.org/dev/peps/pep-0008/) with these specifics:

```python
# Good: Descriptive variable names
stress_probability = model.predict_proba(X_test)[:, 1]

# Bad: Single letter variables
s = model.predict_proba(X_test)[:, 1]

# Good: Clear function names with docstrings
def calculate_vegetation_index(nir, red):
    """
    Calculate NDVI from NIR and Red bands.
    
    Parameters
    ----------
    nir : array-like
        Near-infrared band values
    red : array-like
        Red band values
        
    Returns
    -------
    ndarray
        NDVI values ranging from -1 to 1
    """
    return (nir - red) / (nir + red)
```

### Jupyter Notebook Guidelines

1. **Cell organization**
   - Use markdown cells to explain each section
   - Keep code cells focused (one logical operation per cell)
   - Clear outputs before committing

2. **Comments**
   - Add inline comments for complex logic
   - Use markdown for explanations

3. **Visualizations**
   - Include titles and labels on all plots
   - Use consistent color schemes
   - Add legends where applicable

### Commit Messages

Follow the [Conventional Commits](https://www.conventionalcommits.org/) format:

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

Types:

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Formatting changes
- `refactor`: Code refactoring
- `test`: Adding tests
- `chore`: Maintenance tasks

Examples:

```
feat(model): add SVM classifier comparison
fix(data): handle missing values in moisture index
docs(readme): update installation instructions
```

---

## Reporting Bugs

### Bug Report Template

```markdown
**Describe the bug**
A clear and concise description of what the bug is.

**To Reproduce**
Steps to reproduce the behavior:
1. Open notebook
2. Run cell X
3. See error

**Expected behavior**
A clear description of what you expected to happen.

**Screenshots**
If applicable, add screenshots to help explain your problem.

**Environment:**
 - OS: [e.g., Windows 11]
 - Python version: [e.g., 3.12]
 - Jupyter version: [e.g., 7.0]
 - Package versions (run `pip freeze`)

**Additional context**
Add any other context about the problem here.
```

---

## Suggesting Enhancements

### Enhancement Request Template

```markdown
**Is your feature request related to a problem?**
A clear description of what the problem is. Ex. I'm always frustrated when [...]

**Describe the solution you'd like**
A clear description of what you want to happen.

**Describe alternatives you've considered**
A clear description of any alternative solutions or features you've considered.

**Additional context**
Add any other context or screenshots about the feature request here.
```

---

## Questions?

If you have questions that aren't covered here, please:

1. Check existing [issues](https://github.com/AvirupRoy2195/AI-Based-Crop-Health-Capstone/issues) for similar questions
2. Open a new issue with the `question` label

---

## Recognition

Contributors will be recognized in:

- The README.md acknowledgments section
- Release notes for significant contributions

Thank you for contributing! 🌾

---

<div align="center">

**Happy Contributing! 🚀**

</div>
