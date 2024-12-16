# Account integration flow

### Installing OpenGPT

**Clone the Repository:**  
   Obtain the project files by cloning the repository.

   ```
   git clone https://github.com/langchain-ai/opengpts.git
   cd opengpts
   ```

The following instructions assume you have Python 3.11+ installed on your system.

If you are using `pyenv`, you can create a new virtual environment with:
```shell
pyenv install 3.11
pyenv virtualenv 3.11 opengpts
pyenv activate opengpts
```

Once your Python environment is set up, you can install the project dependencies:

The backend service uses [poetry](https://python-poetry.org/docs/#installation) to manage dependencies.

```shell 
pip install poetry
pip install langchain-community
```

**Install Postgres and the Postgres Vector Extension**
```
brew install postgresql pgvector
brew services start postgresql
```

**Configure persistence layer**

The backend uses Postgres for saving agent configurations and chat message history.
In order to use this, you need to set the following environment variables:

```shell
export POSTGRES_HOST=localhost
export POSTGRES_PORT=5432
export POSTGRES_DB=opengpts
export POSTGRES_USER=postgres
export POSTGRES_PASSWORD=...
```

**Create the database**
```shell
createdb opengpts
```

**Connect to the database and create the `postgres` role**
```shell
psql -d opengpts
```

```sql
CREATE ROLE postgres WITH LOGIN SUPERUSER CREATEDB CREATEROLE;
```

**Install Golang Migrate**

Database migrations are managed with [golang-migrate](https://github.com/golang-migrate/migrate). 

On MacOS, you can install it with `brew install golang-migrate`. Instructions for other OSs or the Golang toolchain, 
can be found [here](https://github.com/golang-migrate/migrate/blob/master/cmd/migrate/README.md#installation).

Once `golang-migrate` is installed, you can run all the migrations with:
```shell
make migrate
```

This will enable the backend to use Postgres as a vector database and create the initial tables.


**Install backend dependencies**
```shell
cd backend
poetry install

```

### Running the application

 Obtain the project files by cloning the repository.

   ```
   git clone 
   cd AGENT
   ```

`python agent.py`
