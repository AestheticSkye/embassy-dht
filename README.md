# Embassy DHT Sensor Library

  This Rust library provides an interface for interacting with DHT1X and DHT2X temperature and humidity sensors using the Embassy framework.

Only test on raspberry pico (w) (RP2040)

 rp2035 may be work

# Getting Started

## Installation

Add embassy-dht-sensor to your Cargo.toml:

```toml
[dependencies]
embassy-dht- = "0.1.0"
```
## Usage

  Initialize your Raspberry Pi Pico board with Embassy. Create an instance of DHTSensor with the GPIO pin connected to your DHT sensor. Use the read method to get temperature and humidity readings.

## Example

```rust
  //   for dht22
  use embassy_executor::Spawner;
  use defmt::*;
  use embassy_time::{Delay, Timer};
  use embassy_rp;
  use embassy_dht::dht22::DHT22;
 
  #[embassy_executor::main]
    async fn main(spawner: Spawner) {
    info!("Hello World!");
 
    let p = embassy_rp::init(Default::default());
 
    info!("set up dhtxx pin");
 
    let mut dht_pin = DHT22::new(p.PIN_22,Delay);
 
    loop {
    Timer::after_secs(1).await;
    let dht_reading = dht_pin.read().unwrap();
    let (temp, humi) = (dht_reading.get_temp(), dht_reading.get_hum());
    defmt::info!("Temp = {}, Humi = {}\n", temp,humi);
    ... the code what you write
 }
 }
```
```rust
  // for dht11
  use embassy_executor::Spawner;
  use defmt::*;
  use embassy_time::{Delay, Timer};
  use embassy_rp;
  use embassy_dht::dht11::DHT11;
 
  #[embassy_executor::main]
    async fn main(spawner: Spawner) {
    info!("Hello World!");
 
    let p = embassy_rp::init(Default::default());
 
    info!("set up dhtxx pin");
 
    let mut dht_pin = DHT11::new(p.PIN_22,Delay);
 
   loop {
    Timer::after_secs(1).await;
    let dht_reading = dht_pin.read().unwrap();
    let (temp, humi) = (dht_reading.get_temp(), dht_reading.get_hum());
    defmt::info!("Temp = {}, Humi = {}\n", temp,humi);
    ... the code what you write
   }
   }
```


Pick up idea from https://crates.io/crates/embassy-dht-sensor