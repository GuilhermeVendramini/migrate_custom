## Este módulo é um exemplo de migração de uma fonte não Drupal

# Coloque o seguinte código no settings.php:

// Note the key 'migrate' here is important.
$databases['migrate']['default'] = array (
 // The database that contains the source data we're going to import.
 'database' => 'database_name',
 'username' => 'user',
 'password' => 'pass',
 'prefix' => '',
 'host' => 'localhost',
 'port' => '3306',
 'namespace' => 'Drupal\\Core\\Database\\Driver\\mysql',
 'driver' => 'mysql',
);


## Drush commands supported include:

migrate-status - Lists migrations and their status.
migrate-import - Performs import operations.
migrate-rollback - Performs rollback operations.
migrate-stop - Cleanly stops a running operation.
migrate-reset-status - Sets a migration status to Idle if it's gotten stuck.
migrate-messages - Lists any messages associated with a migration import.

Examples:
 migrate-import --all                      Perform all migrations                                        
 migrate-import --group=beer               Import all migrations in the beer group                       
 migrate-import --tag=user                 Import all migrations with the user tag                       
 migrate-import --group=beer --tag=user    Import all migrations in the beer group and with the user tag 
 migrate-import beer_term,beer_node        Import new terms and nodes                                    
 migrate-import beer_user --limit=2        Import no more than 2 users                                   
 migrate-import beer_user --idlist=5       Import the user record with source ID 5

Argumentos:
 migration                                 ID of migration(s) to import. Delimit multiple using commas.

Opções:
 --all                                     Process all migrations.                                                                                              
 --execute-dependencies                    Execute all dependent migrations first.                                                                              
 --feedback                                Frequency of progress messages, in items processed                                                                   
 --force                                   Force an operation to run, even if all dependencies are not satisfied                                                
 --group                                   A comma-separated list of migration groups to import                                                                 
 --idlist                                  Comma-separated list of IDs to import                                                                                
 --limit                                   Limit on the number of items to process in each migration                                                            
 --tag                                     Name of the migration tag to import                                                                                  
 --update                                   In addition to processing unprocessed items from the source, update previously-imported items with the current data

Aliases: mi


## DICA:

# Habilite o módulo os módulos "config_update" e "config_update_ui" para registrar as alterações do install .yml


## Comandos para migrar os conteúdos

# Taxonomias:

drush mi custom_tags

# USER:

drush mi custom_user

# FILES 

drush mi custom_files


## ESTRUTURA EXEMPLO UTILIZADA:

# DATA BASE

create database oldsite;


# TAXONOMIAS

CREATE TABLE categories (
	cid int,
	name varchar(255),
	description varchar(255)
);

INSERT INTO categories (cid,name,description)
VALUES (1,'educacão','desc educacão');

INSERT INTO categories (cid,name,description)
VALUES (2,'esporte','desc esporte');

INSERT INTO categories (cid,name,description)
VALUES (3,'economia','desc economia');

INSERT INTO categories (cid,name,description)
VALUES (4,'política','desc política');


# USUÀRIOS

CREATE TABLE users (
	uid int,
	name varchar(255),
	email varchar(255),
	pass varchar(255),
	login varchar(255)
);

INSERT INTO users (uid,name,email,pass,login)
VALUES (1,'Laura','laura@teste.com','123','laura');

INSERT INTO users (uid,name,email,pass,login)
VALUES (2,'Carol','carol@teste.com','1234','carol');


# ARQUIVOS

CREATE TABLE files (
	fid int,
	file_name varchar(255),
	file_filepath varchar(255)
);

INSERT INTO files (fid,file_name,file_filepath) 
VALUES (15,'teste.jpg','sites/default/files/teste.jpg');


