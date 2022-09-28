Environment Variables

Environment variables are variables that store data in your program but outside your code.
For example, key and secret for an API. I want this information to be stored outside my source code, so I can keep sensitive data safe. 
I don't want to expose my credentials inside my open-source code. In addition, I don’t want to touch my code each time API credentials have changed. 
I can access already set environment variables like “USER” for example, using os.environ["USER"] or os.environ.get("USER")
I can add my own environment variable like: os.environ['API_USER'] = 'username'
Cool for now.
When I create a new environment variable, it only exists for that session. When I close the terminal/program, the environment variable no longer exists.
How can I make these variables persist?

My preferred way is to use python-dotenv library
First install the library 
pip3 install python-dotenv
then create a .env file in the same directory as the Python file resides. 
Next, create a variable inside .env file like this:
Name = value 
Back into the code, I will import the library 
from dotenv import load_dotenv
calling load_dotenv function, brings environment variables into os.environ, and now I can access them.
print(os.environ["API_USER"])

Cool for now.
What if I have two environments, each has its own keys. How can I verify Production environment is using Production keys and Development environment is using Development keys?
I can specify more than one .env file, and direct load_dotenv to locate the correct .env file.

For example:
    home = Path().absolute()
    dev_path = Path(f'{home}/DEV/.env')
    prod_path = Path(f'{home}/PROD/.env')

when I want to load the Development environment keys, I will use 
load_dotenv(dotenv_path=dev_path)
    print(os.environ.get("API_KEY"))
    
and when I want to load the Production environment keys, I will use 
load_dotenv(dotenv_path=prod_path)
    print(os.environ.get("API_KEY"))

By default, load_dotenv doesn't override existing environment variables, so either I can use different keys
For example:
API_KEY_DEV in Development .env file and 
API_KEY_PROD in Production .env file

Or in case I want to use the same key in both .env files, I will need to call load_dotenv with override=True to allow overriding the environment value 


