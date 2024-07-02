# COATI-Model-Evaluation
This repository contains all necessary materials and code for replicating the experiments and analyses presented in my report on the [COATI model](https://github.com/terraytherapeutics/COATI). It includes detailed scripts and notebooks for training the model from scratch using the GuacaMol dataset, conducting linear probing tasks, and analyzing molecular generation capabilities.

# Setup Installation

1. **Clone the Repository:**
   Clone the repository to your local machine to get started with the setup.

   ```bash
   git clone https://github.com/StefanHangler/COATI-Model-Evaluation.git
   cd molecule-generation
   ```

2. **Create and Activate a Virtual Environment:**
   - For Unix/macOS systems:
     ```bash
     python3 -m venv env
     source env/bin/activate
     ```
   - For Windows:
     ```bash
     python -m venv env
     .\env\Scripts\activate
     ```

3. **Install the Package:**
   Install the package using `pip` which will handle all dependencies automatically.

   ```bash
   pip install .
   ```

This will install the COATI-Model-Evaluation package and all required dependencies, setting up the environment for running or extending the application.

# Molecule Generation
This repository contains a Python script for generating molecular structures using various pretrained PyTorch models. The models are implemented following an abstract base class to ensure a consistent interface for molecule generation.

## Features
- Abstract base class for molecule generators to ensure consistency and reusability.
- Predefined classes for generating molecules with specific pretrained models.
- Easy extension to include new molecule generation models.

## Generating Molecules

### Run Script
Execute the main script to generate molecules:
```
python generate_molecules.py
```

This will generate molecules using all configured models and save them to CSV files in the current directory.

### Adding a New Model

To add a new model for molecule generation, follow these steps:

1. **Implement the New Model Class:**
   Create a new Python class that inherits from `MoleculeGenerator`. Implement all abstract methods:
   - `load_model()`: Method to load your model and tokenizer.
   - `generate_molecules()`: Method to generate molecules using the model.

   Example:
   ```python
   class NewModelGenerator(MoleculeGenerator):
       def __init__(self, device, doc_url):
           super().__init__(device)
           self.doc_url = doc_url
           self.model, self.tokenizer = self.load_model()

       def load_model(self):
           # Load your model and tokenizer here
           return model, tokenizer

       def generate_molecules(self, num_molecules=100):
           # Logic to generate molecules
           return generated_molecules
   ```

2. **Integrate the New Model into the Main Script:**
   Instantiate your model in the main script and call the `generate_molecules()` method.
   
   ```python
   new_model = NewModelGenerator(device, model_url)
   molecules = new_model.generate_molecules(100)
   new_model.save_molecules(molecules, "new_model_generated_molecules.csv")
   ```

# License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE) file for details.
