<div align="center">

  <h1><code>snakeriver-clientside</code></h1>

  <strong>Clientside library for the SnakeRiver system</strong>

  <h3>
    <a href="https://rustwasm.github.io/docs/wasm-pack/tutorials/npm-browser-packages/index.html">snakeriver-server</a>
  <br>
  <a href="https://rustwasm.github.io/docs/wasm-pack/tutorials/npm-browser-packages/index.html">slide deck</a>
  <br>
  <a href="https://rustwasm.github.io/docs/wasm-pack/tutorials/npm-browser-packages/index.html">poster</a>
   <br>
  <a href="https://rustwasm.github.io/docs/wasm-pack/tutorials/npm-browser-packages/index.html">project template</a>
  </h3>
</div>

## Project Abstract

Many web applications today are read-heavy, meaning users are much more likely to access information from a server than they are to add new data. This read access is often a queried by the client over an internet connection. Computation to produce the desired read data, often on tables in a relational database, can be costly, and queries that are repeated are especially taxing for systems. Several alternative systems to relational databases exist, including Noria, a streaming dataflow system that stores data in a graph. Data and updates flow through the graph’s operator nodes, essentially precomputing a query's desired information, and are stored in ready to access tables called Views. Although this approach significantly reduces read access speeds, it still fails to circumvent the internet latency that comes with queries and data sent back and forth over the internet. 

SnakeRiver is a system where that dataflow graph exists across both server and client, executing server computation and storing View data in the client itself. Reads are therefore done locally and are incredibly fast. In specific graph scenarios, user-specific processing can also be done in the client, reducing server load and costs. This is achieved with a library of Rust functions that compiles into Web Assembly, allowing the creation of a graph that manipulates data in the browser. In our testing of several read and write scenarios, write speeds were reasonable for expected workloads, while reads remained very fast. Latency per operation was as much 10x faster than a Noria system under comparable workloads, showing that the system succeeds in lowering both latency and server computation in web applications that feature read heavy workloads.

## About

This repository contains the library of functions that operate within the browser to create and manipulate the graph. It also contains the development server that serves the page content, including the HTML, CSS, and JS, or the CDN as referenced in the project poster. 

## Code Structure

- `src/operators`: operators that exist in graph, Root is stateless
- `src/types`: all types represented by enums
- `src/units`: row and change objects
- `src/viewsandgraphs`: the view and graph structures
- `index.js`: content served by CDN, also has in javascript testing that works in tandem with the SnakeRiver-server
- `test`: contains throughput and latency testing for purely clientside values, testing with server requires SnakeRiver-server

## 🚴 Usage

In root directory to compile Rust code into Web Assembly:
```
wasm-pack build
```


In www directory to start up server:
```
npm run start
```


In test directory to run clientside tests:
```
wasm-pack test --headless -chrome
```

