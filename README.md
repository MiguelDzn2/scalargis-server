# Instalação

> git clone https://github.com/scalargis/scalargis-server.git

> cd scalargis-server


### Instalar a aplicação em virtualenv

##### Windows 
> x:\Python3x\python -m venv venv  
> venv\scripts\activate  
> (venv) python -m pip install --upgrade pip

##### Linux
> cd scalargis-server
> sudo apt update
> sudo apt install -y gdal-bin libgdal-dev libproj-dev proj-data proj-bin libgeos-dev
    > Porque obtive um erro que nao encontrava "gdal-config" (e o restante sao dependencias relacionadas ao gdal-bin)
> sudo apt install -y libcairo2-dev pkg-config python3-dev
    > Porque nao bastam as packages do python. E necessario instalar isso no sistema para criar graficos e exportar. Ou seja, apenas se pode instalar as dependencias abaixo depois de instalar as dependencias do sistema aqui.
> sudo apt install postgresql-16-postgis-3
    > Porque caso nao instalemos, quando se inicializar a db o Flask vai se queixar que PostGIS nao esta instalado (e aparenemente sera necessario essa extensao para adicionar capacidades geograficas e espaciais.)

> python3 -m venv venv  
> source venv/bin/activate  
> (venv) pip install --upgrade pip

### Instalar dependências de pyhton

##### Windows
> (venv) pip install -r requirements-win.txt

##### Linux
> (venv) pip install -r requirements.txt
> (venv) pip install setuptools [Porque quando inicializei a db disse que faltava o modulo pkg_resources (que esta dentro do setuptools)]
> (venv) pip install pytz [Porque depois de dar fix ao setuptools, obtive outro import error.]

### Criar base de dados e instalar extensão Postgis  

Criar a base de dados através do pgAdmin ou psql. (Para isso 'e necessario instalar o postgre e o driver do postgre)

O scalargis espera que se tenha:
> Nome da DB: scalargis
> Username : postgres
> Password : postgres

O schema, tabelas etc sera feito com o flask init-db abaixo.


sudo -u postgres psql
CREATE DATABASE scalargis;
(O utilizador postgres ja vem por padrao, mas vem sem pass, pelo que temos de a adicionar.)
ALTER USER postgres PASSWORD 'postgres';
GRANT ALL PRIVILEGES ON DATABASE scalargis TO postgres;
\q


### Inicializar a BD

##### Windows 
> (venv) set FLASK_APP=app.main  
> (venv) set APP_CONFIG_FILE=<config_file_name>    
> (venv) cd scalargis  
> (venv) flask init-db

##### Linux
> (venv) export FLASK_APP=app.main  
> (venv) export APP_CONFIG_FILE=<config_file_name>  (Nao precisa, uma vez que quando o Flask inicia, utiliza o default.py )
> (venv) cd scalargis  
> (venv) flask init-db  

### Executar app

##### Windows 
> (venv) set PYTHONPATH=\<path\>\scalargis-server\scalargis;\<path\>\scalargis-server\scalargis\app   
> (venv) cd web\app  
> (venv) python main.py

##### Linux
> (venv) export PYTHONPATH=/<path\>/scalargis-server/scalargis:/<path\>/scalargis-server/scalargis/app  
> (venv) cd scalargis  
> (venv) python3 app/main.py

### Utilizar a aplicação
Abrir no browser o url http://localhost:5000/mapa

Se não funcionar, é porque falta a instalação do componente cliente.
Ou seja, o Flask já está a correr corretamente, mas falta o frontend. O frontend servirá os arquivos estáticos.


## Instalação de componente cliente

Instalar o repositório da componente cliente ao lado da diretoria scalargis-server 

> git clone https://github.com/scalargis/scalargis-client.git

> cd scalargis_client

> yarn install

