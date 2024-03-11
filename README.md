# Creating a Backup for Apache Superset
If you are not the creator
```bash
sudo su
```
```bash
mysqldump -u root -p --all-databases > all_databases.sql
```
- Copy the database file to your home folder using SCP.

- Log in to the server on the superset environment.
```bash
mysql -u root -p  < all_databases.sql
```
- **You need to add/allow the current IP to access the server/database so that you are able to create connection.**

To decrypt copy the secret_key from the previous server and paste it to the current server

Change directory to superset and then, create a superset config file:
```bash
 touch superset_config.py
```
- Open the config file and paste:
```bash
# Superset specific config
ROW_LIMIT = 5000

# Flask App Builder configuration
# Your App secret key will be used for securely signing the session cookie
# and encrypting sensitive information on the database
# Make sure you are changing this key for your deployment with a strong key.
# Alternatively you can set it with `SUPERSET_SECRET_KEY` environment variable.
# You MUST set this for production environments or the server will not refuse
# to start and you will see an error in the logs accordingly.
SECRET_KEY = 'YOUR_OWN_RANDOM_GENERATED_SECRET_KEY'-previous key from the other server
export SUPERSET_CONFIG_PATH=~/superset/superset_config.py
```
- **Save and Exit.**
- Run the following:
```bash
superset db upgrade
superset init
```





