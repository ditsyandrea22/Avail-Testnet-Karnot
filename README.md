# Avail-Testnet-Karnot
avail-deploy-an-appchain-using-madara-karnot


#UPDATE
```
sudo apt update && sudo apt upgrade -y

```
#Install Rust
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
rustc --version

```
#INSTALL GIT
```
sudo apt install git
```
#INSTALL DOCKER
```
sudo apt install apt-transport-https ca-certificates curl software-properties-common

#Now, let’s download the Docker repository’s GPG key and add it to the system’s APT keyring:

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

sudo apt install docker-ce

sudo systemctl start docker

sudo systemctl enable docker

#Install The Final Dependencies

sudo apt-get update -y && sudo apt-get upgrade -y

sudo apt install build-essential

sudo apt install pkg-config

sudo apt install libssl-dev

sudo apt install clang

sudo apt install protobuf-compiler
```
#Install And Configure Madara-CLI:
```
git clone https://github.com/karnotxyz/madara-cli
cd madara-cli
cargo build --release
```
#Now, we will initialize the setup:
```
./target/release/madara init
```
![image](https://github.com/ditsyandrea22/Avail-Testnet-Karnot/assets/34813777/61a3b266-1fef-4a14-b32d-18e0a9393145)

#A new wallet will now be generated, and the secret key will be stored in the following file path: /root/.madara/app-chains/<APPCHAIN_NAME>/da-config.json. If this is your first time using Avail, you can proceed with this newly generated wallet. However, if you have previous experience with Avail, such as setting up a node or participating in previous Clash of Nodes challenges, you should consider replacing the newly generated wallet with your existing one. To do this, you need to open the existing JSON file using the following command, ensuring you replace <APPCHAIN_NAME> with the app chain name you previously selected:
```
nano /root/.madara/app-chains/<APPCHAIN_NAME>/da-config.json
```
#Next, you should update the value within the “seed” tag with your wallet’s seed phrase and the value within the “address” tag with the address of your existing wallet:

![image](https://github.com/ditsyandrea22/Avail-Testnet-Karnot/assets/34813777/f461c245-3d99-4f1f-8ca3-797051b2a70f)

#Now, press “CTRL + X” to exit the file, then type “Y” to save the changes to the file, and finally, press “Enter” to confirm the file name.

#Opening Required Ports:
```
sudo ufw allow 22
sudo ufw allow 4000
sudo ufw allow 5353
sudo ufw allow 47250
sudo ufw allow 39276
sudo ufw allow 36347
sudo ufw allow 43759
sudo ufw allow 40815
sudo ufw allow 30333
sudo ufw allow 9944
sudo ufw allow 9615
sudo ufw enable
```
#Install Screen
```
sudo apt install screen
```
#Now, let’s create a new screen session to to run processes and manage terminal sessions independently. I named mine “appchain” but feel free to choose something different:
```
Screen -Rd appchain
```
#We will now start out appchain:
```
./target/release/madara run
```
#when asked to choose your AppChain, simply press “Enter.” Please note that this process will take some time as it involves building a total of 1519 packages:

![image](https://github.com/ditsyandrea22/Avail-Testnet-Karnot/assets/34813777/f80f24b3-a40c-4010-aab3-c20ba17cbc1e)

#Once the building process is complete, you’ll be asked to confirm if you’ve funded your wallet through the faucet; if you have, press “Y”. After a few minutes the the process should look like this:

![image](https://github.com/ditsyandrea22/Avail-Testnet-Karnot/assets/34813777/77654940-51ff-4ec0-8007-feaa4d9a7515)

#now exit the session with
```
CTRL + A + D
```
#To re-enter your session:
```
screen -r appchain
```
#Start Your Explorer:
#To begin, let’s first navigate to the root directory, then to the “madara-cli” directory, and finally, initiate the explorer. Replace XX.XX.XX.XX with the IP address of your node. Please execute each command individually for a seamless process:
```
cd
cd madara-cli
./target/release/madara explorer --host=XX.XX.XX.XX
```
```
![image](https://github.com/ditsyandrea22/Avail-Testnet-Karnot/assets/34813777/8b992076-ef27-4b0d-b535-520598732287)
```
#Now, open the explorer in your web browser by entering your IP address, followed by port 4000, like this: http://192.168.123.123:4000, for example. Once your explorer is open, switch to “Testnet” on the right-hand side. You’ll notice many zeros, indicating that the network is currently down. However, this should change once the RPC issues have been resolved. Just make sure to revisit this dashboard regurarely to check on it.
```
![image](https://github.com/ditsyandrea22/Avail-Testnet-Karnot/assets/34813777/2bfb279c-ce2c-4df1-b591-b83177fd6a03)
```
#Now, we need to create a JSON file and fill it with specific content. Begin by opening a blank text file, then paste the following template into it:
```
{
  "name": "my_app_chain",
  "logo": "https://placehold.co/400x400",
  "rpc_url": "https://rpc.mychain.xyz",
  "explorer_url": "https://explorer.mychain.xyz",
  "metrics_endpoint": "https://metrics.mychain.xyz",
  "id": "942ff35e-f048-4d10-ae61-6cb970cad2f0"
}
```
#Ensure you replace the placeholder content with your actual details:

Name: Enter the name of your AppChain
Logo: Upload your logo (it should be 400x400px). I used https://imgbb.com/ for uploading. Ensure you use the direct link ending in .png
rpc_url: Replace this with the IP address of your VPS
explorer_url: Also replace this with the IP address of your VPS
metrics_endpoint: This should be replaced with the IP address of your VPS as well
id: Assign any unique UUID here. For example, I used this website to create one. The value doesn’t hold special meaning — it just needs to be unique.
For guidance, my JSON file looks like this:
```
![image](https://github.com/ditsyandrea22/Avail-Testnet-Karnot/assets/34813777/71854a78-342c-44c7-942c-01bab6bc2178)
```
#Now, save this file to your desktop with the filename structured as <UUID.json>. For example, if your UUID is c9636bf8-4721-4a91-b5f7-f9593fa0d919, name the file c9636bf8-4721-4a91-b5f7-f9593fa0d919.json. Make sure to use the .json extension to ensure proper formatting and recognition.

In the next step, we’ll upload this file to the GitHub repository, which we’re going to fork from “avail-campaign-listing.” So we first need to visit this repository, and click the “fork” button:
```
![image](https://github.com/ditsyandrea22/Avail-Testnet-Karnot/assets/34813777/69bd363a-c2bc-47d9-af1d-fdb007c592d0)
```
#Now, Leave all settings as default and click “Create fork.” This will create a fork of the main branch:
```
![image](https://github.com/ditsyandrea22/Avail-Testnet-Karnot/assets/34813777/119e456e-6dad-4582-85ff-fdb2c92acaea)
```
#Let’s now nagivate into the “app_chains” directory:
```
![image](https://github.com/ditsyandrea22/Avail-Testnet-Karnot/assets/34813777/044d2d95-6ec0-44e3-9838-14af01538677)
```
… and then, click the “Upload file” button located in the top right corner.
```
![image](https://github.com/ditsyandrea22/Avail-Testnet-Karnot/assets/34813777/8e959766-cb94-4763-9301-40eff6e2e982)
```
#Next, click the “Choose your files” button and select the JSON file that we created earlier:
```
![image](https://github.com/ditsyandrea22/Avail-Testnet-Karnot/assets/34813777/473d631a-fbad-4fb0-a6a6-0acf043d2b8e)
```
… and click the “Commit changes” button:
```
![image](https://github.com/ditsyandrea22/Avail-Testnet-Karnot/assets/34813777/ce7a4fef-60a6-4ab9-9d86-34d325b3decf)
```
Afterward, click the “Contribute” button and then proceed to click the “Open pull request” button:
```
![image](https://github.com/ditsyandrea22/Avail-Testnet-Karnot/assets/34813777/2963cb00-5ebf-4c48-9641-9fdfa0f8116e)
```
Now, click create the “Create pull request” button:
```
![image](https://github.com/ditsyandrea22/Avail-Testnet-Karnot/assets/34813777/e0e894b2-612d-4a44-8dc3-8dfc96372851)
```
In the final step, I will set the title as “✨ Adding AppChain ilaNihas” and in the description field, write “This is my first Avail AppChain named ilaNihas”. You will need to customize this and then, click “Create pull request” to complete the process.
```
![image](https://github.com/ditsyandrea22/Avail-Testnet-Karnot/assets/34813777/53087dcf-f1b8-4ce6-8b95-483efd8fcea8)
```
#Check the Clash of Nodes leaderboard

If we’ve done everything correctly, our pull request should be automatically merged, and our AppChain should appear on the official leaderboard. To verify, visit https://leaderboard.availproject.org/, check the “Madara leaderboard” tab, and confirm your AppChain is listed. If your pull request isn’t auto-merged, consult the readme file of the Github repository for guidance: https://github.com/karnotxyz/avail-campaign-listing.

Possible reasons for a failed merge might be:

Relevant ports aren’t open
The explorer isn’t reachable → verify by opening http://<YOUR_IPADRESS>:4000/ in your browser
The metrics page isn’t reachable → confirm by accessing http://<YOUR_IPADRESS>:9615/metrics/ in your browser
Your JSON file isn’t correctly formatted → rectify this using the “Prettier” extension in VSCode or the “prettier” command in Ubuntu systems, e.g., npx prettier@latest - write 125a148b-989b-4101-be31–67a63084f77e.json.
![image](https://github.com/ditsyandrea22/Avail-Testnet-Karnot/assets/34813777/a76aee84-1dca-420a-a3cb-69f12f4cdbaa)

#Get the AppChain Builder role
![image](https://github.com/ditsyandrea22/Avail-Testnet-Karnot/assets/34813777/e880aea6-ed4e-48fa-9979-f0cee193865f)

#This enables you to claim 25 AVL tokens per day and up to 200 AVL tokens per week using the following command. This support makes it more convenient to manage your AppChain and conduct testing to contribute to the project:
```
/deposit-rollup <YOUR_ADDRESS>
```
#scure 
```
https://medium.com/@ilaNihas/avail-deploy-an-appchain-using-madara-karnot-373981c2fe9d
```


















