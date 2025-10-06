# Software-Defined Networking (SDN) - Intelligent Traffic Control

This project demonstrates the power of Software-Defined Networking through intelligent traffic redirection and control using Mininet and Ryu SDN controller framework.

## Project Overview

Building an intelligent network traffic control system that dynamically manages data flows in a virtualized network environment. This project showcases how SDN separates network control from data forwarding, enabling programmable and adaptive network behavior.

## Network Architecture

### Topology
- **1 Client**: Sends requests to servers
- **2 Servers**: Handle client requests
- **1 SDN Switch**: Centrally controlled via Ryu controller
- **Ryu Controller**: Implements custom traffic control logic

```
     Client
        |
    SDN Switch
      /    \
  Server1  Server2
```

## Key Features

### 1. Network Topology Setup (`networkTopo.py`)
- Creates virtual network using Mininet
- Configures hosts with custom MAC and IP addresses
- Establishes SDN switch with OpenFlow protocol
- Connects to remote Ryu controller

### 2. Normal Forwarding Mode (`ryu_forward.py`)
- Standard flow-based forwarding
- Learns MAC addresses dynamically
- Implements table-miss flow entries
- Direct packet routing to destinations

### 3. Intelligent Redirection Mode (`ryu_redirect.py`)
- **Traffic redirection logic**: Transparently routes traffic to alternative servers
- **Load balancing**: Distributes load when primary server is overloaded
- **Failover support**: Automatically switches to backup server on failures
- **Flexible routing**: Programmable rules for different traffic types

## Technologies Used

- **Mininet**: Network emulation platform
- **Ryu Framework**: Python-based SDN controller
- **OpenFlow 1.3**: Protocol for SDN communication
- **Python**: Core programming language

## Implementation Details

### Network Configuration
- **Network**: 10.0.1.0/24
- **Client**: 10.0.1.5 (MAC: 00:00:00:00:00:03)
- **Server1**: 10.0.1.2 (MAC: 00:00:00:00:00:01)
- **Server2**: 10.0.1.3 (MAC: 00:00:00:00:00:02)

### Controller Modes

**Normal Forwarding**:
- Direct path: Client → Server1
- Standard MAC learning and forwarding

**Intelligent Redirection**:
- Redirected path: Client → Server2 (transparently)
- Maintains connection integrity
- No client-side configuration required

## How to Run

### Prerequisites
```bash
# Install Mininet
sudo apt-get install mininet

# Install Ryu
pip install ryu
```

### Starting the Network

**Terminal 1: Start Ryu Controller (Normal Mode)**
```bash
ryu-manager ryu_forward.py
```

**Terminal 1: Start Ryu Controller (Redirect Mode)**
```bash
ryu-manager ryu_redirect.py
```

**Terminal 2: Start Mininet Network**
```bash
sudo python3 networkTopo.py
```

### Testing Traffic Control

In Mininet CLI:
```bash
# Ping test
mininet> client ping server1

# Performance test
mininet> iperf client server1

# Network information
mininet> net
mininet> links
```

## Performance Analysis

### Metrics Measured
- **Latency**: Round-trip time comparison
- **Throughput**: Data transfer rates
- **Packet Loss**: Connection reliability

### Expected Results
- Normal forwarding: Direct path with minimal latency
- Intelligent redirection: Slight overhead but enhanced flexibility

## Key Concepts Demonstrated

### SDN Principles
- **Centralized Control**: Network intelligence in controller
- **Programmable Dataplane**: Flow rules dynamically installed
- **Separation of Concerns**: Control plane vs. data plane

### OpenFlow Operations
- Flow table management
- Packet matching rules
- Action execution (forward, drop, modify)

### Network Management
- Dynamic topology adaptation
- Traffic engineering
- Service chaining possibilities

## Use Cases

### Real-World Applications
1. **Data Center Networks**: Load balancing across servers
2. **Cloud Infrastructure**: VM migration and traffic optimization  
3. **Network Function Virtualization**: Flexible service insertion
4. **Disaster Recovery**: Automatic failover to backup systems

## Project Structure

```
Software-Defined-Networking/
├── README.md
├── networkTopo.py          # Mininet network topology
├── ryu_forward.py          # Normal forwarding controller
└── ryu_redirect.py         # Intelligent redirection controller
```

## Technical Highlights

- **MAC Learning**: Dynamic address resolution
- **Flow Installation**: Proactive and reactive flow setup
- **Packet Processing**: Custom handling in controller
- **State Management**: Tracking network state

## Educational Value

This project demonstrates:
- SDN architecture and OpenFlow protocol
- Network virtualization with Mininet
- Python programming for network control
- Performance testing and analysis
- Modern cloud networking concepts

Perfect for understanding how modern data centers and cloud providers manage network traffic programmatically.

## Team Members

- **Rui Sang**
- **MingXuan Hu**
- **ZiQi Liu**
- **ZhiXin Li**
- **ZhengHao Zhou**

## Course Information

- **Course**: CAN201 - Computer Networks
- **Institution**: Xi'an Jiaotong-Liverpool University
- **Year**: 2024

## References

- [Mininet Documentation](http://mininet.org/)
- [Ryu SDN Framework](https://ryu-sdn.org/)
- [OpenFlow Specification](https://www.opennetworking.org/software-defined-standards/specifications/)

## License

This project is developed for educational purposes as part of coursework.

