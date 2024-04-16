这是一个C++编写的 web3 windx86插件
可以提供给 C/C++ Delphi 易语言 等非解释性语言调用

支持交易签名带data 
支持消息签名

例子
   Eth* eth = ETH_Create();
   ETH_SetInfo(eth, "https://127.0.0.1", "58");
   //查询余额；
   ETH_GetBalance(eth,"0xBeEDBF1d1908174b4Fc4157aCb128dA4FFa80942");
   //获取GasPrice
   const char * GasPrice = ETH_GetGasPrice(eth);
    //交易签名
   struct TradeInfo {
  	const char* to;
  	const char* value;
  	int chainId;
  	const char* gasPrice;
  	int gasLimit;
  	int nonce;
  	const char* data;
    };
    
   TradeInfo tradeInfo = {
     "0x12345677890",
     StringtoWei("0.0001"), //1ETH=1000000000000000000wei
     112358,
    "317440400",
     21000,
     99,
     ""
     };
     const char* SignTrans = ETH_SignTransaction(eth, &tradeInfo, "0x1234567890abcdef12345678903736351c79efa95282e6bbd92801a876543210");
     //发送交易
     ETH_SendSignedTransaction(eth, SignTrans);
    //消息签名
    ETH_SignMsg(eth,Sha3Raw("Hello World"), "0x1234567890abcdef12345678903736351c79efa95282e6bbd92801a876543210");

    //ETH_GetChainId(eth);
    //ETH_PrivateKeyToAddress(eth,"0x1234567890abcdef12345678903736351c79efa95282e6bbd92801a876543210");
    //ETH_GetNonce(eth,"0xBeEDBF1d1908174b4Fc4157aCb128dA4FFa80942");

    //PRC_Send
    const char* str = "{\"id\" : 1, \"jsonrpc\" : \"2.0\", \"method\" : \"eth_getBalance\", \"params\" : [\"0xBeEDBF1d1908174b4Fc4157aCb128dA4FFa80942\", \"latest\"] }";
    ETH_PrcSend(eth, str);
  
