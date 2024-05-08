# Selectable PDF stack

The Selectable PDF stack provides the infrastructure to convert PDFs, especially 
scanned PDFs (i.e. where the text cannot be selected) into Selectable PDF 
(i.e. where the text can be selected).

## Prerequisites

To deploy this stack, you need:
* An AWS account
* Python 3.8 or higher: [Lambda Python Runtimes](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html)
* [AWS CLI](https://aws.amazon.com/cli/): configured with` AWS configure`
* [AWS CDK](https://aws.amazon.com/cdk/): version 2.X or higher

You can find the instruction to install and configure these prerequisites [here](https://docs.aws.amazon.com/cdk/latest/guide/getting_started.html#getting_started_prerequisites).

You also need to boostrap your CDK on your AWS account. This need to be done only 
once! The bootstrapping information are available [here](https://docs.aws.amazon.com/cdk/latest/guide/getting_started.html#getting_started_bootstrap).

## Prepare the CDK environment

This project is set up like a standard Python project.  The initialization process 
also creates a virtualenv within this project, stored under the .venv directory.  
To create the virtualenv it assumes that there is a `python3` executable in your 
path with access to the `venv` package. If for any reason the automatic creation 
of the virtualenv fails, you can create the virtualenv manually once the init 
process completes.


> [!IMPORTANT]
> The virtualenv you create in the following step should match the Python version that the
lambdas will utilize. A mismatch between the local build and the lambda run
will result in dependency errors with PyMuPDFlike [this](https://github.com/keithrozario/Klayers/issues/168).


To manually create a virtualenv on MacOS and Linux:
```
$ python3 -m venv .venv
```

After the init process completes and the virtualenv is created, you can use the 
following step to activate your virtualenv.
```
$ source .venv/bin/activate
```
Always activate virtualenv when working with CDK on this stack.

Once the virtualenv is activated, update pip (the installation setup needs the newest 
version of pip, so don't forget this step!), then install the package.
```
$ pip install pip --upgrade
$ pip install .
```

You might want to force reinstallation if some changes in `setup.py` are not taken 
into account during a standard installation
```bash
$ pip install . --force-reinstall
```

### Useful CDK commands

 * `cdk ls`          list all stacks in the app
 * `cdk synth`       emits the synthesized CloudFormation template
 * `cdk deploy`      deploy this stack to your default AWS account/region
 * `cdk diff`        compare deployed stack with current state
 * `cdk docs`        open CDK documentation

## Deploy the Annotation stack with CDK
In the folder of this README.md, open the file `app.py` and update the stack name 
and the stack description if required. Then run
```bash
$ cdk deploy
```
Which will output
```
 ✅  stack-name

Outputs:
stack-name.DocumentInputBucket = stack-name-inputdocuments<UID>
stack-name.DocumentOutputBucket = stack-name-processeddocuments<UID>
stack-name.ProcessingLogsDynamoDB = stack-name-Documents<UID>
```
`stack-name-inputdocuments<UID>` is the bucket where you can upload your PDFs 
and `stack-name-processeddocuments<UID>` is the bucket where the selectable version 
of your PDFs will be located.




