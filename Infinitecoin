import os
import platform

from twisted.internet import defer

from . import data
from p2pool.util import math, pack

nets = dict(
   infinitecoin=math.Object( #IFC Coin
        P2P_PREFIX='fcc1b7dc'.decode('hex'),#add by guugll - its described in this thread
        P2P_PORT=9321,#add by guugll - coin port
        ADDRESS_VERSION=102,#add by guugll - its described in this thread
        RPC_PORT=9322,#add by guugll - coin port
        RPC_CHECK=defer.inlineCallbacks(lambda bitcoind: defer.returnValue(
            'infinitecoinaddress' in (yield bitcoind.rpc_help()) and
            not (yield bitcoind.rpc_getinfo())['testnet']
        )),
        SUBSIDY_FUNC=lambda height: 1000*100000000 if height>1000 else 100*100000000,
        POW_FUNC=lambda data: pack.IntType(256).unpack(__import__('ltc_scrypt').getPoWHash(data)),
        BLOCK_PERIOD=30, # s,duo shao miao ,yi ge block
        SYMBOL='IFC',
        CONF_FILE_FUNC=lambda: os.path.join(os.path.join(os.environ['APPDATA'], 'infinitecoin') if platform.system() == 'Windows' else os.path.expanduser('~/Library/Application Support/infinitecoin/') if platform.system() == 'Darwin' else os.path.expanduser('~/.infinitecoin'), 'infinitecoin.conf'),
        BLOCK_EXPLORER_URL_PREFIX='http://exploretheblocks.com:2750/block/',
        ADDRESS_EXPLORER_URL_PREFIX='http://exploretheblocks.com:2750/address/',
        TX_EXPLORER_URL_PREFIX='http://exploretheblocks.com:2750/tx/',
        SANE_TARGET_RANGE=(2**256//1000000000 - 1, 2**256//1000 - 1),
        DUMB_SCRYPT_DIFF=2**16,
        DUST_THRESHOLD=0.03e8,
    ),
)
for net_name, net in nets.iteritems():
    net.NAME = net_name
