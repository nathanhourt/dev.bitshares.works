
**************
Testnets
**************

BitShares offers a live Public Testnet that is open for anyone to join which allows arbitrary testing without using real BTS.  Instead, users transact and pay fees using the Testnet's core asset, TEST.  The Public Testnet is a great space to start learning about BitShares-Core features and BitShares-UI wallet, without needing to buy or risk valuable BTS. 

To use the BitShares Testnet, check out the **testnet** branch from the BitShares-Core repository. This branch can be built and run in the same way as the **master** or **develop** branches, but it will connect to and interact with the Public Testnet instead of the main BitShares network.

**The testnet branch** includes bug fixes or new features which have not yet been released to the main network.

-------------

Public Testnets
-------------------------

To access the BitShares Public Testnet, simply download and build BitShares-Core's **testnet** branch, then use this version the same way as the normal BitShares software. Software built from the testnet branch will connect with the Public Testnet instead of the main network.

To register an account on the Testnet and receive TEST asset, go to https://testnet.bitshares.eu/. This is a public Wallet UI and Faucet for the Testnet. It will allow users to create new accounts, and it will fund created accounts with some initial TEST asset.


.. toctree::
    :maxdepth: 2

    testnets/public_testnet
 
-------------  
  
Private Testnets
-------------------------


While the Public Testnet is useful for experimenting with existing BitShares functionality, or for testing upcoming features prior to release on the main BitShares network, it is instead necessary to create a private testnet to test new hardforking changes, or to control the behavior of privileged accounts such as witnesses or committee accounts. A private testnet is a brand new blockchain which starts and produces blocks on a single node, although more nodes can be added later as desired. Although a private testnet cannot utilize the existing infrastructure of the Public Testnet, such as witness nodes and web wallet GUIs, they allow much more powerful testing of the blockchain functionality as the developer has total control of all accounts on the chain.

Any branch in the BitShares-Core repository may be used to launch a private testnet; however, if the intent is to develop changes which will be submitted to upstream BitShares for inclusion in the main network, it is best to begin from the **hardfork** branch, as all hardforking pull requests must be submitted to this branch. Alternatively, the **master** branch may be used as a stable base which reflects the current release of BitShares, or the **develop** branch may be used to gain the latest changes from BitShares development as they are posted.

To launch a private testnet, use a custom genesis block which creates the initial blockchain witness accounts with keys the developer controls, then launch ``witness_node`` with the custom genesis and configured to produce blocks using the initial witness accounts and keys. The ``witness_node`` should begin producing blocks at #1 and continue producing blocks as long as it runs. This node can be stopped and started at will, although the testnet will be down while this node is stopped, and when restarting, the last several blocks produced may be lost.

While the private testnet is running, other nodes may be connected, and block production can be decentralized across these nodes to simulate a more realistic blockchain network. Additionally, wallets or other interfaces can be connected to the blockchain node(s) to publish transactions and query chain state.


.. toctree::
    :maxdepth: 2
 
    testnets/private_testnet
  

-----------  
 
  
Other References 
------------------

* :ref:`how-to-setup-python-lib`

  - How to Create MPAs/UIAs with Python
  

* :ref:`Set up Faucet <how-to setup-faucet>`
* :ref:`Set up Nignx <how-to-setup-nignx>`
* :ref:`Code Coverage Testing (wiki) <how-to-testing-bts>`
* :ref:`How to verify block production <veryfy_block_production>`
* :ref:`How to backup a server <witness-backup-server>`
* :ref:`How witness Price Feeds work <witness-price-feeds>`
* :ref:`explorer-wrappers`
* :ref:`public-testnet-guide-2`
	
	
-------


|
