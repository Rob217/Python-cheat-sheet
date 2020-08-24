# Virtual environments

Useful resources:
- https://packaging.python.org/tutorials/installing-packages/
- https://www.youtube.com/watch?v=N5vscPTWKOk

Steps for creating and using a virtual environment:
1. Create a directory in which your virtual environment is going to be stored, e.g., ```test_env_dir```
```bash
> mkdir test_env_dir
> cd test_env_dir
```
2. Inside that directory, create a new virtual environment using the ```virtualenv``` package
```bash
> python -m virtualenv test_env
```
3. Activate this new environment
```bash
> test_env/Scripts/activate
```
4. Notice now that `[test_env]` is at the start of the command line indicating you are in the new environment and can load and install Python packages as required.
```bash
(test_env) >
```
5. To exit the virtual environment type:
```bash
(test_env) > deactivate
```
