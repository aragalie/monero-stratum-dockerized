
This is largely based on [@PedroD's monero-stratum-docker](https://github.com/PedroD/monero-stratum-docker). He hasn't updated it in many months, so i thought of having here a working version of it (as of Dec '17).

# Purpose

A docker which will allow you to solo mine using any monero miner, be it CPU or GPU (literally any miner that works with a stratum pool).


## Requirements

- A monero-based wallet+daemon
- Docker installed
- Miner of choice (eg. xmr-stak-nvidia, ccminer, etc)

## How it works
By running `start.sh`you are automatically creating a [Monero Stratum pool](https://github.com/sammy007/monero-stratum.git) in your local machine, inside the Docker instance.

You can then connect any miner you like to this pool by pointing it to localhost:3333 (or remote_ip:3333 if your miner is on another computer).

Just remember to edit the `configs.json` with your wallet's address and upstream address. The upstream address is where the pool gets the blockchain and its real-time updates (to read and submit new blocks).

In practice this means you need to have `monerod` (monero daemon, or any other monero-based daemon) running somewhere (in the local machine where the pool is running for eg.), as that gets the latest blocks from the network and also submits the hashes.


For many wallets, if it is your first time using it, you'll have to download the entire blockchain via the daemon and/or their website (it will time as the files are large) and make sure the the GUI is updated and fully synchronized to the network.



## Steps

1. Install your monero-based wallet GUI.
2. Download the blockchain for your wallet and make sure that it is fully syncronized. 
3. Change the address in the `config.json` file to your wallet receive address.
4. Run `sh start.sh` (if on Windows, make sure you have Git-Bash installed for PowerShell and/or Cygwin, otherwise the file won't execute properly)
5. Your docker instance will start building so wait (it will take quite some time)
6. When the machine is done setting up and running, and you start seeing logs like `2017/12/25 23:56:51 Loading config: /monero-stratum/config.json` or messages related to Batches being sent to miners, you're now ready (pool is working and waiting for workers)
5. Configure any miner of your choice (eg. xmr-stak-nvidia, ccminer, etc) and configure it to use this stratum, for eg. my miner was configured this way: `ccminer -o stratum+tcp://192.168.0.108:3333 -u <your wallet address here>`, where `192.168.0.108` is the IP of the machine running this docker container, which could also be `localhost`.
6. You can also activate the solo mining option in the Advanced tab on your monero-based Wallet-gui to add CPU mining as well
7. Take a look at `http://localhost:8082/` in the machine where you're running the container, and the Stratum dashboard with details will be visible
8. Enjoy your solo mining!

**Note:** You can add more miners, and if you are able to host this online you can create your own online private pool!

## Acknowledgements

Thanks again to [@PedroD](https://github.com/PedroD/) for creating the initial Docker file and writing the instructions and to [@Sammy007](https://github.com/sammy007/) for the Monero-Stratum tool itself.


### Donation Bitcoin address:
16fXENJGoPNfFik5vUmC5PrDk87DUepVG

### Donation Verge address:
DMSRzCj9E5gQsB4CjesSQd93gsCdi6dQt1

### Donation Ethereum address:
0xF00df12CB9Eb8Bc9c15Bfd7c75c3FD37E0f6CF48

### Donation Electroneum address:
etnk6YiVFAy1VRSxVQhfHnezv3YNHueqe9xk71WDdr16frH9a3aStdmSUYQqfxQpiCbLXiED5diubd666u1fLrbe6F9WAHNkZ6

### Donation Bulwark address:
bGRtx8SPrirDApusN3enrHLQyif8M46WyJ



