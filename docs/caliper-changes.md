### Changes made to original Caliper code:<br>

*  Caliper client was missing out certain block events at higher transaction rates resulting in failed transactions. This was because the Caliper client itself was single threaded and was performing both functions of sending transactions as well as listening to events resulting from transaction confirmations. We modified the client to spawn a new process that essentially splits the listener and processor into separate processes. A newly spawned process only listens to block events and inserts them in a messaging queue to be processed later by Caliper's main process. By having a separate process listen continuously to block events, we have completely eliminated occurrence of failed transactions due to missed block events at higher transaction rates. 

* The code to read the path of the client private keys were hardcoded in the caliper. Changes were made to read the path from the blockchain network configuration file.
