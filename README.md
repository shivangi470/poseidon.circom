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

Here's a step-by-step example of a complete workflow using the --name flag for contributions:

    Powers of Tau Ceremony:

    bash

snarkjs powersoftau new bn128 12 pot12_0000.ptau
snarkjs powersoftau contribute pot12_0000.ptau pot12_0001.ptau --name="Initial Contributor" -v
snarkjs powersoftau contribute pot12_0001.ptau pot12_0002.ptau --name="Second Contributor" -v
snarkjs powersoftau prepare phase2 pot12_0002.ptau pot12_final.ptau

Phase 2 Ceremony:

bash

snarkjs groth16 setup poseidon.r1cs pot12_final.ptau poseidon_0000.zkey
snarkjs zkey contribute poseidon_0000.zkey poseidon_final.zkey --name="Phase 2 Contributor" -v

Export Verification Key:

bash

snarkjs zkey export verificationkey poseidon_final.zkey verification_key.json

Generate Witness:

bash

snarkjs calculatewitness --wasm poseidon_js/poseidon.wasm --input input.json --witness witness.wtns

Generate Proof:

bash

snarkjs groth16 prove poseidon_final.zkey witness.wtns proof.json public.json
snarkjs groth16 verify verification_key.json public.json proof.json

Generate Solidity Verifier:

bash

snarkjs zkey export solidityverifier poseidon_final.zkey verifier.sol

function parameter: snarkjs zkey export soliditycalldata public.json proof.json