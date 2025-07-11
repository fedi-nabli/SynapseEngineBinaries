# Synapse Engine

Welcome to the official Synapse AI Engine official docker image.

## Overview

Synapse AI Engine is a new initiative aimed to simplify AI models training, generation and inference for newcomers and education.

## Stack

The project uses a mixture of Zig, C, C++ and Rust for different components and uses CMake as the central build system.

## SYNJ

SYNJ is a DSL (Domain Specific Language) aiming to reduce the frontier of AI modeling to newcomers, student and hobbiests. The language (as shown below) defines the model, architecture and different parameters for the AI model.

```code
model_name = "Celsius To Farenheit";
algorithm = LinearRegression;
csv_path = "./tests/ctf.csv";
train_test_split = [80, 20];
target = "Farenheit";
features = ["Celsius"];
epochs = 1600;
learning_rate = 0.1;
batch_size = NULL;
early_stop = { "patience": 1400 };
output_path = "./tests/ctf_model.json";
```

## Examples and Usage

The engine now have only LinearRegression and MultiLinearRegression models implemented with more to come.
Please also note that the implemented algorithm also accepts only numberical data.

The repository contains an EngineTest default folder that has two real-world examples with the CSV data and config file (SYNJ)

The first example is Celsius To Farenheit. the ctf.csv and ctf_config.synj files are the CSV Data and DSL Config file respectively.

To run the example, you can either use the the files already existing or copy this config file:
```synj
model_name = "Celsius To Farenheit";
algorithm = LinearRegression;
csv_path = "./tests/ctf.csv";
train_test_split = [80, 20];
target = "Farenheit";
features = ["Celsius"];
epochs = 1600;
learning_rate = 0.1;
batch_size = NULL;
early_stop = { "patience": 1400 };
output_path = "./tests/ctf_model.json";
```

The second example is California House Pricing dataset. It contains 20,640 entries and 8 features. The housing.csv and housing_config.synj are the CSV Data and DSL Config file respectively.

To run the example, you can also use the preconfigured config file or copy this config file:

```synj
model_name = "California Housing Price";
algorithm = LinearRegression;
csv_path = "./tests/housing.csv";
train_test_split = [80, 20];
target = "median_house_value";
features = [
  "longitude",
  "latitude",
  "housing_median_age",
  "total_rooms",
  "total_bedrooms",
  "population",
  "households",
  "median_income"
];
epochs = 400;
learning_rate = 0.5;
batch_size = 64;
early_stop = { "patience": 20 };
output_path = "./tests/housing_model.json";
```

## Usage

Synapse is a CLI tool and offers 5 commands:

These commands are:

- help (Shows help message and for each commands shows usage)
- dump (Shows trained model data)
- predict (Run raw inference on new data for a trained model)
- train (Train a model given the configuration and data files)
- version (Print current version and related release data)

## Usage Breakdown

To run the command simple run, this will just print a generic usage message:
```bash
synapse
```

To print version data, run one of the following:
```bash
synapse version
syanspe --version
synapse -V
```

To show more detailed help and usage message, you run run either of the following:
```bash
synapse help
synapse --help
synapse -h
```

All commands support two ways for flag handeling either by putting the flag, a space, then the value or by putting the flag=value.

These two commands are the same:
```bash
synapse dump --file=./tests/ctf_model.json
synapse dump --file ./tests/ctf_model.json
```

To train a model, you use the ```train``` subcommad. It in turn offers more helper
To see the detailed usage of the train command, run one of the following:
```bash
synapse train --help
synapse train -h
```

To train a model, you need to give it the configuration file via the ```--config``` (can be used in short version of ```-C```) flag.
For example, to train the Celsius to Farenheit model, you need to run one of the following
```bash
synapse train --config ./ctf_config.synj
```

The train command also offers two flags ```verbose``` and ```dump``` which prints the data of each epoch and shows the final model data respectively.

A full training command might look something like this:
```bash
synapse train -C ./ctf_config.synj --dump --verbose
```

After a trained model output it's final data, you can use the ```predict``` command to run raw inference on some data
The predict command offers help command for detailed usage, simple run either of the following:
```bash
synapse predict --help
synapse predict -h
```

The command requires two flags, one for the outputed model data via the ```--json``` or ```-J``` flag and the input values via the ```--input``` or ```-I``` flag.
Note: for the input, if it starts with a negative number either wrap it in quotes or use '=' right after the flag without spaces.

A predict command for the trained Celsius To Farenheit model above can be executed in either of the following ways:
```bash
synapse predict --json ./tests/ctf_model.json --input 70
synapse predict --json ./tests/ctf_model.json --input=70
synapse predict --json ./tests/ctf_model.json --input "70"
synapse predict -J ./tests/ctf_model.json -I 70
```

Finally, the dump command takes the outputed file as a paramter via the ```--file``` or ```-F``` flag and print the model data.
It also offers a help command, to see detailed usage, simple run either of these:
```bash
synapse dump --help
synapse dump -h
```

A full dump command for the trained Celsius to Farenheit model looks like either of these:
```bash
synapse dump --file ./tests/ctf_model.json
synapse dump -F ./tests/ctf_model.json
```

## Contact

If you have issues running the image, about the usage or have questions or feedback, don't hesitate to conctact me at the following:

Email: `fedinabli@gmail.com`

[LinkedIn](https://www.linkedin.com/in/fedi-nabli-76670219a/)

[Facebook](https://www.facebook.com/fedi.nabli.3)
