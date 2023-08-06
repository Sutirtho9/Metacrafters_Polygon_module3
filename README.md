# Polygon zkSNARK Circuit Implementation: Logical Operations

## Description:
Welcome to the GitHub repository for the Polygon zkSNARK Circuit Implementation! In this project, we aim to design and deploy a Zero-Knowledge Succinct Non-Interactive Argument of Knowledge (zkSNARK) circuit on the Polygon blockchain network. The circuit will implement a custom logical gate, enabling secure and privacy-preserving computations.

The primary objective of this repository is to develop a circuit using the circom programming language, a popular choice for zkSNARK circuit design due to its efficiency and flexibility. The logical gate implemented within the circuit will allow users to perform specific confidential operations while keeping sensitive inputs hidden from public scrutiny.

## Getting Started

### Installation

To work with this project, you need to follow these steps:

1. Download the Circom programming language from the official website: [Circom](https://www.circom.io/).
2. Install Circom on your system by following the instructions provided in the documentation.

### Executing the Program

To run the circuit, follow these steps:

1. Open your terminal or command prompt and navigate to the project directory.
2. Compile the circuit by executing the following command:

bash
npm install


3. After successful installation , Compile the Circuit:

bash
npx hardhat circom 


4. Deployment:  I am deploying the circuit on the Polygon Mumbai testnet , you can use any testnet 

bash
npx hardhat run scripts/deploy.ts --network mumbai



## Circuit Logic

The circuit logic is implemented using Circom and consists of three templates for the basic logic gates: AND, OR, and NOT. The main custom circuit 'LooseCircuit' is constructed using these gates.

### AND Gate

The AND gate template takes two input signals, 'a' and 'b', and produces the output signal 'out', representing the logical AND of 'a' and 'b'.

circom
template AND() {
    signal input a;
    signal input b;
    signal output out;

    out <== a * b;
}


### OR Gate

The OR gate template takes two input signals, 'a' and 'b', and produces the output signal 'out', representing the logical OR of 'a' and 'b'.

circom
template OR() {
    signal input a;
    signal input b;
    signal output out;

    out <== a + b - a * b;
}


### NOT Gate

The NOT gate template takes an input signal 'in' and produces the output signal 'out', representing the logical NOT of 'in'.

circom
template NOT() {
    signal input in;
    signal output out;

    out <== 1 + in - 2 * in;
}


### Custom Circuit - Multiplier2

The main custom circuit 'Multiplier2' uses the AND, NOT, and OR gates to implement the logic for multiplying inputs 'a' and 'b' and producing the output 'q'.
```
pragma circom 2.0.0;

/*This circuit template checks that c is the multiplication of a and b.*/  

template Multiplier2 () {  

    // signal inputs A and b
    signal input a;
    signal input b;
    

    // Signals from the gates 
    signal x;
    signal y;


    // final signal output 
    signal output q;


    // The components which we will be using 

    component andGate = AND();  
    component orGate = OR();  
    component notGate = NOT(); 

    //circuit logic


    
    andGate.a <== a;
    andGate.b <== b;

    x <== andGate.out;


    

    notGate.in <== b;

    y <== notGate.out;


    

    orGate.a <== x;
    orGate.b <== y;

    q <== orGate.out;




}


// Below are the templates of the gates i will be using in my circuit logic 

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

component main = Multiplier2();
```


After following the installation and execution steps, the circuit will be successfully implemented, and you will obtain the desired output 'q' based on the inputs 'a' and 'b'.

## Help
If you encounter any issues or have questions about the program, please refer to the official Circom documentation or seek help from the community.

# Author
[Sutirtho Chakravorty](https://www.linkedin.com/in/sutirtho-chakravorty-239214231/)

License
This project is licensed under the MIT License.
