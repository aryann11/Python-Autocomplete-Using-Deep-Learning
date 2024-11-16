# Python Autocomplete

This is a learning/demo project to show how deep learning can be used to auto complete Python code.
You can experiment with LSTM and Transformer models.
We also have built a simple VSCode extension to try out the trained models.

It gives quite decent results by saving above 30% key strokes in most files, and close to 50% in some. We calculated key
strokes saved by making a single (best)
prediction and selecting it with a single key.

The dataset we use is the python code found in repos linked in
[Awesome-pytorch-list](https://github.com/bharathgs/Awesome-pytorch-list). We download all the repositories as zip
files, extract them, remove non python files and split them randomly to build training and validation datasets.

We train a character level model without any tokenization of the source code, since it's the simplest.

### Try it yourself

1. Clone this repo
2. Install requirements from `requirements.txt`
3. Run `python_autocomplete/create_dataset.py`.
    * It collects repos mentioned in
      [PyTorch awesome list](https://github.com/bharathgs/Awesome-pytorch-list)
    * Downloads the zip files of the repos
    * Extract the zips
    * Remove non python files
    * Collect all python code to `data/train.py` and, `data/eval.py`
4. Run `python_autocomplete/train.py` to train the model.
   *Try changing hyper-parameters like model dimensions and number of layers*.
5. Run `evaluate.py` to evaluate the model.

### VSCode extension

1. Clone this repo

2. Install requirements from `requirements.txt`

3. Install npm packages

You need to have [Node.JS](https://nodejs.dev/) installed

```shell
cd vscode_extension
npm install # This will install the NPM packages
```

4. Start the server `python_autocomplete/serve.py`

5. Open the extension project (folder) in [VSCode](https://code.visualstudio.com/)

```shell
cd vscode_extension
code . # This will open vscode_extension in VSCode
```

If you don't have [VSCode command line launcher](https://code.visualstudio.com/docs/setup/mac#_launching-from-the-command-line)
start VSCode and open the project with `File > Open`

6. Run the extension from VSCode

```
Run > Start Debugging
```

This will open another VSCode editor window, with the extension

7. Create or open a python file and start editing!

### Sample

Here's a sample evaluation of a trained transformer model.

Colors:

* <span style="color:yellow">yellow</span>: the token predicted is wrong and the user needs to type that character.
* <span style="color:blue">blue</span>: the token predicted is correct and the user selects it with a special key press,
  such as TAB or ENTER.
* <span style="color:green">green</span>: autocompleted characters based on the prediction

<p align="center">
  <img src="/images/python-autocomplete.png?raw=true" width="100%" title="Screenshot">
</p>
