# poseidon.circom

use by entropy


                9e63a5f6,2b96538d,aaed2372,481920d1
                a40b9195,9ea38ef9,f5f6a303,3b886516
                0710d067,c09d0961,5f928ea5,17bcdf49
                ad75abd2,c8340b40,0e3b18e9,


Step-by-Step Process

    Compile the Circuit:
    Make sure you have already compiled the circuit and generated the necessary files:

    bash

circom poseidon.circom --r1cs --wasm --sym

Ensure the poseidon.wasm file is generated in the correct folder.

Create the Input File:
Create the input.json file in your project directory with the required inputs. For example:

json

{
  "inputs": [1, 2]
}

Generate the Witness:
Navigate to your project directory and run the snarkjs command with the correct path to the .wasm file:

bash

snarkjs calculatewitness --wasm poseidon_js/poseidon.wasm --input input.json --witness witness.wtns

Verify the Witness (Optional):

bash

snarkjs wtns debug poseidon_js/poseidon.wasm witness.wtns poseidon.sym

Generate the Solidity Verifier (After Trusted Setup and Proof Generation):
