# Lightning Network node operators experience random`force-close` of payment channels (in high fee environment)

https://github.com/lightningnetwork/lnd/pull/7609

Lightning Network node operators are continuously exploring various tools and techniques to enhance network performance and reliability. One such operator, [SunnySarah](https://twitter.com/SunnySarahNode/status/1655137367487807488), has shared their experiences and tuning suggestions on different forums and social media platforms and discussed Alex Bosworth's suggestions to reduce the force-close channel event. Alex has contributed to the development of HTLC Interceptors and suggested various tuning methods. Bosworth has been an active contributor to Lightning Network development and developed LND software, widely used for implementing the Lightning Network protocol.

[AlexBosworth](https://twitter.com/alexbosworth/status/1651236610829172748) recommends increasing the Time Lock Delta and doubling the CLTV delta and max-cltv-expiry value to mitigate certain attacks. If channels were created with older software, operators need to modify each channel to the recommended new defaults.

## How to Increase Time Lock Delta in Channel Policy

To increase the Time Lock Delta in the channel policy for each of your Lightning Network channels in LND, you can use the updatechanpolicy command. This command allows you to modify the channel policy settings for a specific channel, including the Time Lock Delta value.

To increase the Time Lock Delta to 120 blocks, you would run the following command:


```lncli updatechanpolicy <channel_point> --min_htlc=1000 --max_htlc=500000000 --fee_rate=0 --time_lock_delta=120```

In this command, <channel_point> should be replaced with the channel point of the channel you wish to modify. The --min_htlc and --max_htlc flags are used to set the minimum and maximum HTLC values for the channel, respectively, while the --fee_rate flag sets the fee rate for the channel.

Finally, the --time_lock_delta flag is used to set the Time Lock Delta value for the channel. In this example, it is set to 120 blocks.

It's worth noting that increasing the Time Lock Delta value can impact the usability and flexibility of the channel, as it will increase the amount of time required to complete transactions. Therefore, it's important to carefully consider the implications of modifying this value and ensure that it aligns with your overall strategy and goals for using the Lightning Network.

## How to Update the Routing Policies to Double the CLTV Delta

To update the routing policies to double the CLTV delta and the max-cltv-expiry value in LND, you can use the updatechanpolicy command with the --cltv_delta and --max_cltv_expiry flags.

To double the CLTV delta, you can run the following command:

```   
lncli updatechanpolicy <channel_point> --cltv_delta=80 --max_cltv_expiry=2016
```

In this command, <channel_point> should be replaced with the channel point of the channel you wish to modify. The --cltv_delta flag sets the new CLTV delta value, which is twice the default minimum value of 40. The --max_cltv_expiry flag sets the maximum CLTV expiry value to 2016, which is twice the default maximum value of 1008.

By setting the --cltv_delta and --max_cltv_expiry flags to the appropriate values, you can increase the CLTV delta and the max-cltv-expiry value for the channel, respectively. This can help to ensure that your channel remains usable and flexible even as CLTVs continue to increase on the Lightning Network.

You can set the cltv_delta and max_cltv_expiry values in your lnd.conf file using the following configuration options:

```

[chan_policy]
cltv_delta=80
max_cltv_expiry=2016
```
These options will set the default channel policy for all channels. If you want to set the policy for a specific channel, you can use the lncli updatechanpolicy command with the --chan_point flag, like this:

```css

lncli updatechanpolicy --chan_point=<channel_point> --cltv_delta=80 --max_cltv_expiry=2016
```
Note that <channel_point> should be replaced with the funding transaction ID and output index of the channel in the format txid:index.


The benefits of doubling the CLTV (CheckLockTimeVerify) value in the Lightning Network, as proposed in pull request #7609 on the LND GitHub repository, include increased flexibility and usability of Lightning Network channels. By doubling the CLTV value, Lightning Network nodes and channel operators can help to ensure that their channels remain functional and accessible even as CLTV values continue to increase.

Specifically, doubling the CLTV value can help to mitigate against the risk of expired payments due to increasing CLTV values. With higher CLTV values, it can take longer for transactions to be confirmed on the Bitcoin blockchain, which can lead to payments expiring before they can be completed. By doubling the CLTV value, channels will be better equipped to handle these longer confirmation times and ensure that payments are able to be completed successfully.

Additionally, doubling the CLTV value can help to increase the number of available routes for payments on the Lightning Network, as channels with higher CLTV values will be able to forward payments with higher CLTV values. This can help to reduce the likelihood of payment failures and increase the overall efficiency and reliability of the Lightning Network.

## Mempool Flooding and CLTV value 

Increasing the CLTV value for Lightning Network channels can help to increase the safety window in the event of node downtime. When a node goes offline or experiences other connectivity issues, its channels may become unresponsive, and any payments that were in progress at the time may become stuck or fail. By increasing the CLTV value, channel operators can give themselves more time to recover from node downtime before these payments expire, which can help to reduce the risk of payment failures and lost funds.

Additionally, increasing the CLTV value can add some buffer room around time locks, which may become more stressed in the future assuming the current mempool load remains persistent. The mempool is the queue of unconfirmed transactions on the Bitcoin network, and during periods of high demand, it can become congested, which can lead to longer confirmation times and higher CLTV values. By increasing the CLTV value now, channel operators can help to ensure that their channels remain usable and flexible even as the mempool load increases.

Mempool flooding, which has been ongoing for a while, has led to extremely high transaction fees and increased transaction confirmation times on the Bitcoin network. This has made it difficult for Lightning Network users to open and close channels, and has led to some channels being force-closed due to expired time locks. Therefore, while increasing the CLTV value can be a beneficial strategy in general, it may not be sufficient to fully address the challenges posed by the current mempool load.

Overall, while the Lightning Network offers a highly secure and efficient way to conduct off-chain Bitcoin transactions, it is still a rapidly evolving technology, and developers and operators must remain vigilant against potential attacks and vulnerabilities.