# VoteTrackerPlus

VoteTracker+ (VTP) is a 100% open software ballot tracking system that increases the security, accuracy, and trustworthiness of paper ballot based elections by cryptographically tracking the paper ballots.  VTP is a software only product comprised of backoffice plugins with voter and election official facing frontoffice components.  VTP can leverage existing election hardware infrastructure to the extent that the OEM manufacturers allow and support the installation of the VTP plugins.

## 1) Overview

VoteTracker+ is a distributed, open-source ballot and Cast Vote Record ([CVR](https://pages.nist.gov/ElectionGlossary/#cast-vote-record)) integrity and tracking system to support public [elections](https://en.wikipedia.org/wiki/Election). It enables verifiable, accurate, secure and transparent elections with full voter based [End-to-end](https://en.wikipedia.org/wiki/End-to-end_auditable_voting_systems) verifiable (E2EV) ballots.  VoteTracker+ maximizes the transparency and trust of an election throughout the election process by:

* allowing each voter to verify that their ballot is electronically cast, collected, and counted as intended
* allowing each voter and all election officials to verify the tally of all the ballot questions
* allowing each voter to inspect their neighborhood for fraudulent voters and/or addresses
* allowing each voter and all election officials to inspect all the voter names and addresses across the entire electorate for possible voter and ballot fraud
* cryptographically associating the anonymous paper ballots with the anonymous VoteTracker+ digital copies, insuring that neither set is tampered or fraudulently altered as well as supplying a third copy directly to the voter themselves, thus creating 3 separate copies of the anonymous but cryptographically signed ballot data

VoteTracker+ is an open source distributed database/repository and application that supports:

* full End-to-End validation (E2EV) of the paper and digital ballots
* storing all the digitally interpreted scans of the paper ballots in a secure and anonymous manner
* executing the tally of all the races via 100% open source software contained within the same repositories as the ballot data
* creating blank ballots as a function of address
* (Aspirationally) storing the address and name of all the voters who cast a ballot without the association of any other information - the ballots are 100% anonymous
    * Ideally, if there is a previous election, VoteTracker+ would track the voter's name and address across elections allowing greater insight and transparency into potential voter and election fraud


VoteTracker+ is NOT a:

* voter ID solution
* voter registration solution
* ballot scanner nor contains ballot scanning software - VoteTracker+ receives the interpreted ballot from the ballot scanner, which could be a traditional mechanical scanner, smart phone application, or manually from an election official
* replacement for paper ballots - VoteTracker+ requires the balloting process to start and end with a paper ballot

## 2) Basic 50,000 Foot Overview

The VTP root repo (this repo) is meant to be directly integrated via a git submodule with a VTP ElectionData directory tree which is comprised of one or more git submodules (though as of this writing and stage of agile software development, an OS level symbolic-link is typically used instead).  An VTP ElectionData tree is a directory tree that _componentizes_ the backend election configuration data into separate GGOs (Geopolitical Geographical Overlays - NIST calls this a [geopolitical unit](https://pages.nist.gov/ElectionGlossary/#geopolitical-unit)).  Each GGO can have is its own [RBAC](https://en.wikipedia.org/wiki/Role-based_access_control) authority or share another GGO's RBAC.  Independent of the GGO components the ElectionData tree supports arbitrary git submodule componentization which ultimately allows a [Voting Center](https://pages.nist.gov/ElectionGlossary/#vote-center) to operate completely disconnected from an external computer network.

A sample mock ElectionData repo can be found at [VTP-mock-election.US.01](https://github.com/TrustTheVote-Project/VTP-mock-election.US.01).

Note that for convenience all VTP repos in the [TrustTheVote](https://github.com/TrustTheVote-Project) GitHub domain start with the four letter prefix __VTP-__.

## 3) Additional Details

For a more detailed overview, see the file [./docs/project-overview.md](./docs/project-overview.md) in this git repo.  The docs folder also contains the current [pitch](./docs/pitch.md) as well as an [informal security description](./docs/informal-security-description.md).

VoteTracker+ is intended to be compliant to the sensible extent possible [NIST](https://en.wikipedia.org/wiki/National_Institute_of_Standards_and_Technology)'s [voting](https://www.nist.gov/itl/voting) efforts.

VoteTracker+ will attempt to leverage as much code and prior art as possible. There are several possible alternatives for standing up a pilot; if you have suggestions please get in touch.

## <a name="ElectionGuardb"></a>4) Other Voting Solutions

The following is a short and incomplete list of other voting projects that are of relevance:

* [ElectionGuard](https://freeandfair.us/electionguard/) 
* [Helios Voting](https://heliosvoting.org/) 
* [Pret-a-Voter](https://en.wikipedia.org/wiki/Pr%C3%AAt_%C3%A0_Voter) 
* [Scantegrity](https://en.wikipedia.org/wiki/Scantegrity) 
* [STARVote](https://www.usenix.org/conference/evtwote13/workshop-program/presentation/bell) 
* [VotingWorks](https://www.voting.works/) (and [VotingWorks Suite](https://docs.voting.works/vxsuite/))

The differences between ElectionGuard and VoteTracker+ and that of blockchain technologies in general is worth a special note.  ElectionGuard is based on the paper [Simple Verifiable Elections](https://www.usenix.net/legacy/events/evt06/tech/full_papers/benaloh/benaloh.pdf) by Josh Benaloh.  Such solutions are based on independently encrypting the individual CVR's of the ballot (encrypting the ballot data at rest) and with the necessary inclusion of a [Benaloh Challenge](https://github.com/phayes/benaloh-challenge) implementation to add a layer of trust for the voting machines that perform the encrypting.  VTP is less complex in that the CVR's are never encrypted and as such no Benaloh Challenge is required.  Voters get direct access to the real and final per contest CVR digests as the CVRs need not be encrypted since the voter's CVR's are effectively anonymized amongst 99 other sets of contest CVRs.  No encryption / decryption is required for the VTP data-at-rest portion even while significant encryption occurs in the VTP data-in-movement portion much like today's commercial/military grade encrypted network connections.

In addition ElectionGuard is not based on a Merkle Tree as each CVR is independent and not connected with the other CVRs.  VTP adds a significant layer of security and trustworthiness via a Merkle Tree implementation in that the entire change history is stored in the public Merkle Tree ledger.  However, unlike cryptocurrencies which are also Merkle Tree based but which are also based on [blockchain](https://en.wikipedia.org/wiki/Blockchain) technology, VTP is not based on blockchain technology and contains no blockchain [implementation/code](https://github.com/dragonchain/dragonchain).  This again results in VTP being less complex than blockchain solutions while also not subject to the significant issues that blockchains implementations have with voter and ballot anonymity.

Finally, unlike both Benaloh and blockchain voting implementations, VTP is anonymized in time both in an absolute sense, as the ballot data contains no date and time information, and via the Merkle Tree chain itself as the CVRs are randomized in linkage order.

For more information contact Sandy Currier at: sandy at osetinstitute dot org

## 5) Development

See the [bin/README.md](bin/README.md) for notes regarding running and writing code.

## 6) Status - 2022/07/19

VoteTracker+ is currently in the early design phase - still working out the basics and seeking credible peer reviews. The current priorities are:
* Technical peer reviews
* Recruiting contributing developers and UX designers, specifically a javascript engineer to provide a GUI around the current command line based demo
* Developing a crowdfunding campaign

The crowdfunding project is getting closer to launch.  A preliminary project video is available at [https://www.youtube.com/watch?v=V0EuZHNHZ6A](https://www.youtube.com/watch?v=V0EuZHNHZ6A).  The launch is contigent on receiving meaningful peer reviews to independently establish the efficacy and viability of the VoteTracker+ solution and on creating an adequate GUI based demo.
