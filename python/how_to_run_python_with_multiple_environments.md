# How to run python with multiple environments

In order to run python with multiple environments first download [Anaconda](Anaconda).

Then create a new conda environment
```
conda create -n shiny_new_env python=3.4
```

Then list the current created environments
```
conda env list
```

Then activate the environment
```
conda activate shiny_new_env
```

Now create a new clean requirement txt file
```
pip freeze > requirements.txt
```

To exit this environment
```
conda deactivate
```

Run the following code if pip installation conflicts are giving you trouble.
```
conda install -r requirements.txt
```


[reference](https://boscacci.medium.com/why-and-how-to-make-a-requirements-txt-f329c685181e)
