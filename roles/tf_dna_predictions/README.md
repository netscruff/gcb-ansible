# Setup transcription factor DNA predictions website
For use with a server with docker already installed.

Creates a database for holding predictions.
 
Downloads prediction and model lists based on predictionconf.yaml config file (in TF-DNA-PredictionsDB).
Loads the database with the prediction and models.
The download and load are only done once. 
This is controlled via the existence of /pred_data/loaded.txt.

Starts web portal (https://github.com/Duke-GCB/TF-DNA-PredictionsDB) and vacuum daemon to cleanup database.
Starts prediction worker for creating custom predictions based on users uploaded sequences(https://github.com/Duke-GCB/Predict-TF-Binding-Worker)
The web port creates jobs and the worker processes them. 
The worker communicates with the web port via its REST API.

The database, portal, vacuum daemon, and worker all run in docker containers.

# How to test against research toolkits
### Create research toolkit (rapid-173.vm.duke.edu for this example).

### Copy your key onto the server: 
```
ssh-copy-id -i ~/.ssh/id_rsa.pub rapiduser@rapid-173.vm.duke.edu
```
### Add server to inventory
```
...
[tf_dna_predictions]
rapid-173.vm.duke.edu ansible_user=rapiduser
...
```
### Run playbook
```
ansible-playbook -i inventory --vault-password-file ~/.vault_pass.txt tf_dna_predictions.yml 
```
If loading the full dataset will take a long time (couple days) to download and load the data into the database the first time.
****
### View website
https://rapid-173.vm.duke.edu

