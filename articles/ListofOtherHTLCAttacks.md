# List of Other HTLC Attacks

Here is a list of known or previous used HTLC attacks on the Lightning Network:

1. Hash Time Locked Contract (HTLC) flooding attack: An attacker floods the network with HTLCs, overwhelming nodes and causing them to close channels to protect their funds.

1. HTLC Interceptor attack: An attacker uses an HTLC interceptor to block, modify, or redirect a payment request, causing the payment to fail or be sent to the wrong recipient.

1. Onion replay attack: An attacker intercepts and replays a valid payment request multiple times, effectively double-spending the payment.

1. Sphinx replay attack: An attacker intercepts and replays a Sphinx packet (used for routing payments on the Lightning Network) multiple times, causing the same payment to be sent multiple times.

1. Payment hash preimage attack: An attacker reveals the preimage (a secret value) of the payment hash associated with an HTLC, causing the recipient to receive the payment before fulfilling the conditions of the HTLC.

1. Probing attack: An attacker probes the network for information about payment channels, such as their balances, routing policies, and fees, in order to exploit weaknesses and carry out other attacks.

It is important to note that the Lightning Network is still in development and new attack vectors may be discovered in the future. Developers are constantly working to improve the security and resilience of the network against these and other types of attacks.
# Onion Replay Attack Attacks

Another type of attack involving HTLCs on the Lightning Network is known as the "Onion Replay Attack".

In this attack, the attacker intercepts and captures a valid payment request sent through the Lightning Network, and then replays it multiple times. Because the payment request is encrypted and routed through multiple nodes, it is difficult for the network to detect and prevent these replayed payments.

To carry out this attack, the attacker must be able to intercept the payment request at a specific point in the network, typically at a routing node. They can then store the encrypted payment request and replay it multiple times at a later time, effectively double-spending the payment.

To mitigate this attack, the Lightning Network uses a technique called "replay protection". This involves adding a random "payment hash" to each payment request, which must be unique for each payment. This makes it difficult for an attacker to replay a payment request, as the payment hash would no longer be valid.

However, if an attacker is able to intercept a payment request before the payment hash is added, they may still be able to carry out an onion replay attack. To prevent this, it is important to ensure that routing nodes on the Lightning Network are secure and trusted, and to monitor the network for any unusual activity or traffic. Additionally, developers are exploring new techniques and protocols to further enhance the security and resilience of the Lightning Network against onion replay attacks and other types of HTLC attacks.