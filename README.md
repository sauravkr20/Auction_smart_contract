# Setup

1. Install [Docker Desktop](https://www.docker.com/products/docker-desktop)
2. Install [Algorand sandbox](https://github.com/algorand/sandbox)
3. Add this project folder as bind volume in sandbox `docker-compose.yml` under key `services.algod`:
    ```yml
    volumes:
      - type: bind
        source: <path>
        target: /data
    ```
4. Start sandbox:
    ```txt
    $ ./sandbox up
    ```
5. Install Python virtual environment in project folder:
    ```txt
    $ python -m venv venv
    $ source ./venv/Scripts/activate # Windows
    $ source ./venv/bin/activate # Linux
    ```
6. Use Python interpreter: `./venv/Scripts/python.exe`
    VSCode: `Python: Select Interpreter`

# Auction

1. to compile the Pyteal to Teal 
    run ```txt 
        $ ./build.sh contracts.counter.auction
        ```

2. to run in sandbox 
- first create the app 
    ```txt
    goal app create --creator $CREATOR_ADDR --approval-prog /data/build/approval.teal --clear-prog /data/build/clear.teal --global-byteslices 2 --global-ints 3 --local-byteslices 0 --local-byteslices 0 --local-ints 0
    ```

- then call the app accordingly using 
     ```txt
    goal app call --app-id $APP_ID --from $FROM_ADDRESS {FOLLOWED BY APP ARGUEMENTS}
    ```

## App Arguement Structure 

- arg[0] stores the op
- args[1] stores the nft_id_key
- args[2] stores the time_delay
- args[3] is min_bid


## understanding the Contract 
- the contract.py stores the contract scripts written in Pyteal which when compiled generates the Teal code .
