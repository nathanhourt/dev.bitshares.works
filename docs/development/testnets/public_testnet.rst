
.. _public-testnet-guide:

************************
Public Testnet Set up
************************

In this section, we are going to build and start a node on the BitShares Public Testnet. For the Public Testnet, you should checkout the **testnet** branch from the BitShares-Core Github repository.


.. contents:: Table of Contents
   :local:
   
-------


This document provides a generic overview of the build process. We also provide more detailed installation guides for different OSes. For these guides, go to :ref:`Installation Guide <installation-guide>`.


1. Installation
----------------------

1-1. Download the Source files
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Let's get started! First, open a **command line interface (CLI) window** and go to a directory where you wish to download the BitShares repository. Now, run the following command lines:

 ::
 
    git clone https://github.com/bitshares/bitshares-core.git --recursive -b testnet bitshares-core-testnet
    cd bitshares-core-testnet/

This will clone bitshares into the ``bitshares-core-testnet`` directory, along with all submodules, and checkout the **testnet** branch, then change directories into the repository.

1-2. Initial Compilation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Now that we've cloned the repository, let's build the programs. Run the following commands. This will build two programs, ``witness_node`` and ``cli_wallet``. 

 ::

   cmake .
   make witness_node cli_wallet

You can find the compiled program binaries in the below folders. 

.. list-table::
   :widths: 20 80
   :header-rows: 1
   
   * - Program
     - Path
   * - witness_node 
     - programs/witness_node/witness_node
   * - cli_wallet 
     - programs/cli_wallet/cli_wallet

	 
|

--------------

2. Configuration
----------------------------------------------------

Upon first launch, ``witness_node`` will create a data directory which contains the persistent blockchain data as well as a configuration file named ``config.ini``.

At this point, we just want a default configuration. :ref:`See here  <bts-config-ini-eg-public-testnet>` for a more detailed overview of the config file and options.

Run the following command and press ``[Ctrl]+C`` after a few seconds to exit.

:: 
   
   ./programs/witness_node/witness_node

This will create a directory, ``witness_node_data_dir``, in the current directory. This directory contains the ``config.ini``, a ``logging.ini``, and some folders for data storage. These folders are not intended for manual modification.

Alternatively, you may specify a different data directory like so:

::
   
   ./programs/witness_node/witness_node -d /path/to/data/dir
	  

|

----------------


3. Start the Testnet (witness_node)
--------------------------------------

Now you know the testnet directory structure and some of important files. Let's start the testnet! 

::

   ./programs/witness_node/witness_node 
   
   
If you want to use own data directory, do not forget to set the parameter ``--data-dir``! Otherwise, the default data directory ``witness_node_data_dir`` will be created to use in your current directory. 
   
::
   
   ./programs/witness_node/witness_node --data-dir data/testnet


   
If you want to use the ``cli_wallet``, you need to specify at least the rpc endpoint. For instance, 

::

    ./programs/witness_node/witness_node --rpc-endpoint "127.0.0.1:8090"

 
|

---------------

4.  Create a Testnet Account 
----------------------------------------------------

4-1. Preparation for CLI wallet
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
(If you have your testnet accounts already, you can jump this section.)

We want to use a BitShares Public UI wallet for testnet(http://testnet.bitshares.eu/) to register new testnet account. The public UI wallet has been set the faucet (https://faucet.testnet.bitshares.eu/) already. The faucet address is used to pay the registration fee for new users! (*To learn more details, please refer BitShares Users Guide.*)

  1) Go to the Public testnet UI wallet: (http://testnet.bitshares.eu/) to create new testnet account.
  2) If you see "Application initialization issues", try to select "Public Testnet Server (...)" from a FULL NODE API SERVER dropdown list. 
  3) Click a [CREATE ACCOUNT] button to register a new testnet account. 
  4) Save your password and Create an account.
  5) If the new account was created successfully, you will receive some asset TEST for the Public Testnet transactions.
  
4-2. Obtain your wallet key pairs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  
  6) Go to a [Permissions] page and save your new UI wallet Active, Owner, and Memo key pairs (public key and private key).
  7) Keep your private key information securely.

Example Key Pairs (testnet account: ken-test01) 
~~~~~~~~~~~~~~~~~
The below table is Example Owner, Active, and Memo key pairs. Each authority has a public key and a private key. The private key is to be kept securely since it gives you control over a wallet.


.. list-table::
   :widths: 15 10 60
   :header-rows: 1

   * - permissions
     - keys
     - values	 
   * - **Owner**
     - public key
     - TEST5qqct-Test-OWNER-Public-key-jqXfSopvhW5A
   * - 
     - private key
     - 5JRf-Test-OWNER-Private-key-ERGw9zctF8kB
   * - **Active**
     - public key
     - TEST72uQ5-Test-ACTIVE-Public-key-6CKa3fpqrfye
   * -  
     - private key
     - P5KN-Test-ACTIVE-Private-key-Pn3jNVZBh
   * - **Memo**
     - public key
     - TEST5jork-Test-MEMO-Public-key-A91aWDZztyMCaR6
   * -  
     - private key
     - P5J3-Test-MEMO-Private-keyva7C9sYW6

	 
You might've noticed each public key start with **TEST**.  So, you know those private keys are for the testnet. If you create BitShares mainnet account, you will find **BTS** on the top of each private key.

**Note:** The Memo key is for decrypting transfer memos. 
  
|

-------------------
  
5.  Use of CLI wallet in Public Testnet
----------------------------------------------------

In this section, we will connect a ``cli_wallet`` and import an existing testnet account by importing the two private keys into your cli wallet. After we import the testnet account, we will test our first transaction ``transfer`` on the BitShares testnet blockchain.
 
.. Attention:: If you have newly created testnet account and just started a public testnet witness_node, you have to make sure if your node has been synced completely. Otherwise, you will not be able to find your new account data. 
 
  
5-1. Connect cli_wallet
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Let's open new command window. If you have started the public testnet (``witness_node``) with the rpc endpoint (i.e.,"127.0.0.1:8090"), you will be able to connect your ``cli_wallet`` by the following command ::

    ./programs/cli_wallet/cli_wallet -s ws://127.0.0.1:8090

	
5-2. Set a password 
^^^^^^^^^^^^^^^^^^^^^^^

If you are first time connecting the ``cli_wallet``, you will receive a ``set_password`` prompt. That means your cli wallet has been connected successfully to the public testnet witness_node.

We are going to set a password and unlock the ``cli_wallet``. The password is used to encrypt the private keys in the wallet. In the below,*supersecret* is a password. 

* ``set_password`` 

   >>> set_password supersecret

* ``unlock`` the wallet::

   >>> unlock supersecret


After the ``unlock``, we can search and view the existing public testnet accounts data. Let's check if your testnet account is on the public testnet blockchain. We use the following command ``get_account`` to view an account information::
 
      unlocked >>> get_account ken-test01

   
And the following command ``list_account_balances`` to view the balance of the account:: 
  
       unlocked >>> list_account_balances ken-test01


.. note:: If you get errors and cannot find the testnet account, make sure your public testnet node has been synced completely.


If you could find your testnet account successfully, your next step is **importing** your testnet account into the cli wallet. 


5-3. Import your testnet account to a cli_wallet
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^	
In the following section, we use *ken-test01* as a testnet user account to explain easier. You should replace the account by your testnet account. 


We want to import two private keys. First one is **Active Private key** to transfer your fund.    The next one is **Memo Private key** to transfer your memo data.   

      >>> import_key ken-test01 P5KN-Test-ACTIVE-Private-key-Pn3jNVZBh   // Active private key
      >>> import_key ken-test01 P5J3-Test-MEMO-Private-keyva7C9sYW6      // Memo private key

	
* ``import_key`` <name> "<wifkey>"

  - \<name\> is the account name owning the key
  - \<wifkey\> is the private key in WIF format
	

In BitShares Blockchain, balances are contained in accounts. Use the following as an example to import your testnet account balances. These balances can be claimed, with no fee.


      >>> import_balance ken-test01 ["P5KN-Test-ACTIVE-Private-key-Pn3jNVZBh"] true

* ``import_balance`` <name> ["*"] true


After you imported your public testnet account and balances, let's check if you imported them successfully. If you have the public testnet account and balance in the current cli_wallet, it will show the data by the following command.

      >>> list_my_accounts


**Note:**
If you want to check the private key of the current cli_wallet, you can use a command ``get_private_key`` with the pair of the public key. 

	>>> get_private_key  TEST72uQ5-Test-ACTIVE-Public-key-6CKa3fpqrfye	
        P5KN-Test-ACTIVE-Private-key-Pn3jNVZBh
	
	
	
5-4. Transfer funds
^^^^^^^^^^^^^^^^^^^^^^^^^

At this point, We should have your public testnet account into your cli wallet. Let's try to send some funds (testnet asset TEST) from ``ken-test01`` to ``faucet``.  If you know another public testnet account, you can sent a fund to the testnet account. Use the following command ::  	
	
    >>> transfer ken-test01 faucet 10 TEST "" true                     // without Memo
    >>> transfer ken-test01 faucet 25 TEST "Hi, send my TEST!" true    // with Memo



|
	  
----------
