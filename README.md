# Two-Phase-Commit-Protocol-2PC-Implementation
Introduction
This project involves developing the Two-Phase Commit (2PC) protocol and analyzing its response to node breakdowns using controlled and random failure injections. In the 2PC protocol, there is one transaction coordinator (TC) and at least two participants. Each node (including the TC and participants) employs a timeout mechanism and transitions to either the commit or abort state if no response is received.

Two-Phase Commit Protocol
The 2PC protocol aims to resolve issues in distributed transactions across multiple servers (locations) such as S1, S2, S3, ..., Sn. The main transaction T is divided into sub-transactions T1, T2, T3, ..., Tn, each assigned to a server Si. Each server Si maintains a separate log record for all associated operations. The protocol involves the following phases:

Phase 1: Prepare Phase
Coordinator Log Entry: The coordinator starts by adding a log record to its location.
Prepare Request: The coordinator sends a prepare message to all participating sites where the transaction T was executed.
Participant Response:
Abort Decision: If a site decides to abort, its local transaction manager writes an abort T log record and sends an abort T message to the coordinator.
Commit Decision: If a site decides to commit, its local transaction manager writes a ready T log record and sends a ready T message to the coordinator.
Phase 2: Commit/Abort Phase
Coordinator Decision: The coordinator decides the final outcome based on the responses received:
Commit: If the coordinator receives ready T from all participating sites, it commits T, updates its log, and sends commit T messages to all sites.
Abort: If the coordinator receives abort T from any site or times out, it aborts T, updates its log, and sends abort T messages to all sites.
Participant Action:
Commit: Upon receiving commit T, each site commits the component of T and logs it.
Abort: Upon receiving abort T, each site aborts the component of T and logs it.
Considerations
Each site logs events specific to that site; there is no global log.
The coordinator is crucial in determining the commit or abort of the distributed transaction.
Communication between the coordinator and sites is essential for the protocol.
Each transmitting site logs each message for recovery purposes.
Project Structure
src/: Contains the source code for the 2PC protocol implementation.
tests/: Contains tests for verifying the correctness of the 2PC protocol under various failure conditions.
docs/: Contains documentation and analysis of the 2PC protocol, including responses to controlled and random node breakdowns.
How to Run
Clone the Repository:
bash
Copy code
git clone <repository-url>
cd <repository-directory>
Install Dependencies:
bash
Copy code
pip install -r requirements.txt
Run the 2PC Protocol:
bash
Copy code
python src/main.py
Run Tests:
bash
Copy code
pytest tests/
Analysis
The analysis of the 2PC protocol's response to node breakdowns involves injecting controlled and random failures to observe the behavior of the system. The results are documented in the docs/ directory.

Contributing
Contributions are welcome! Please fork the repository and submit a pull request.

License
This project is licensed under the MIT License. See the LICENSE file for details.

