# zk SNARK Designer
This project demonstarte how to design a new zkSNARK circuit with some logical operations. Then, we need to implement the circuit and deploy a verifier on-chain to verify proofs generated from this circuit.

## Description
For this project, we will create a circuit using the circom programming language that implements the following logical gate given in the below circuit diagram, compile the contract and deploy it to the Mumbai testnet.

### Circuit Diagram

![Circuit Diagram](https://authoring.metacrafters.io/assets/cms/Assessment_b05f6ed658.png?updated_at=2023-02-24T00:00:37.278Z)



### Circuit Code

```
pragma circom 2.0.0;


template MyGateCircuit () {  

   //signal inputs
     signal input a;
     signal input b;

    //signal from gates
     signal  x;
     signal  y;

    //final signal output
    signal output q;

    //component gates used to create custom circuit
    component andGate = AND();
    component notGate = NOT();
    component orGate = OR();

    //circuit logic
     andGate.a <== a;
     andGate.b <== b;
     notGate.in <== b;

     x <== andGate.out;
     y <== notGate.out;

     orGate.a <== x;
     orGate.b <== y;
     q <== orGate.out
}

template AND() {
    signal input a;
    signal input b;
    signal output out;

    out <== a*b;
}

template OR() {
    signal input a;
    signal input b;
    signal output out;

    out <== a + b - a*b;
}

template NOT() {
    signal input in;
    signal output out;

    out <== 1 + in - 2*in;
}

component main = MyGateCircuit();
```
The goal is to prove that you know the inputs A (0) & B (1) that yield a 0 output

## Steps to run this project
Follow the given below steps to run this project on your VS code
 ### 1) Clone the repository
 ### 2) run ***npm i*** in the terminal to install or download all the dependencies required for this project.
 ### 3) create a .env file and store the wallet private key. 
 ### 4) run ***npx hardhat circom*** , to compile the circuit and get the output file as out and also a verifier contract will be created inside contracts folder.
 ### 4) run ***npx hardhat run scripts/deploy.ts --network mumbai*** , to deploy the verifier contract on mumbai Testnet.


 ## Author
 Atish Kumar Shah
 
