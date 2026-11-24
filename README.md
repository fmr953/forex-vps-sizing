# VPS for Forex Trading: How Much RAM Your EA Needs, Which City to Deploy In, and What Evoxt's 11 Plans Cost

If your broker's trade server sits in Equinix NY4, a VPS in Frankfurt will not improve your fills, and extra RAM will not either. Pick the city first, then the RAM, then the price. On Evoxt's published plan table that lands most EA traders on **VM-1 at $5.99/month** (1 core, 2 GB RAM) for one or two terminals, or **VM-2 at $11.99/month** (2 cores, 4 GB) once you run three or more.

What follows: the full Evoxt plan list, the broker-to-datacenter map that decides your location, a RAM-to-terminal conversion you can apply to any provider, and the two setup mistakes that make people conclude their VPS "didn't work".

> **Quick pick:** one or two MT4/MT5 terminals with a handful of charts: VM-1, $5.99/month, deployed in your broker's city. Three to six terminals or indicator-heavy charts: VM-2 at $11.99, or VM-4 at $23.99 if you also run copiers. 👉 [Deploy an Evoxt VM in your broker's city](https://bit.ly/EvoXt)

## All Evoxt plans, prices and specs

Evoxt is a general-purpose cloud VM provider rather than a forex-branded host. Every plan runs on CPUs clocked up to 6.0 GHz, includes weekly offsite backups at no extra cost, and is billed monthly by default with prepay terms up to three years.

| Plan | CPU · RAM · Storage | Monthly transfer | Price / month | Deploy |
| --- | --- | --- | --- | --- |
| VM-0.5 | 1 core · 512 MB · 5 GB | 150 GB | $3.49 | [Deploy VM-0.5](https://bit.ly/EvoXt) |
| VM-0.75 | 1 core · 1 GB · 10 GB | 250 GB | $4.99 | [Deploy VM-0.75](https://bit.ly/EvoXt) |
| VM-1 | 1 core · 2 GB · 20 GB | 300 GB | $5.99 | [Deploy VM-1](https://bit.ly/EvoXt) |
| VM-1.5 | 2 cores · 2 GB · 20 GB | 300 GB | $6.95 | [Deploy VM-1.5](https://bit.ly/EvoXt) |
| VM-2 | 2 cores · 4 GB · 30 GB | 600 GB | $11.99 | [Deploy VM-2](https://bit.ly/EvoXt) |
| VM-3 | 4 cores · 4 GB · 30 GB | 700 GB | $14.99 | [Deploy VM-3](https://bit.ly/EvoXt) |
| VM-4 | 4 cores · 8 GB · 60 GB | 1,000 GB | $23.99 | [Deploy VM-4](https://bit.ly/EvoXt) |
| VM-6 | 8 cores · 8 GB · 60 GB | 1,250 GB | $29.99 | [Deploy VM-6](https://bit.ly/EvoXt) |
| VM-8 | 8 cores · 16 GB · 80 GB | 2,000 GB | $47.99 | [Deploy VM-8](https://bit.ly/EvoXt) |
| VM-12 | 16 cores · 16 GB · 80 GB | 2,500 GB | $60.95 | [Deploy VM-12](https://bit.ly/EvoXt) |
| VM-16 | 16 cores · 32 GB · 100 GB | 4,000 GB | $95.99 | [Deploy VM-16](https://bit.ly/EvoXt) |

Two notes on that table. VM-0.5 and VM-0.75 are too small for MetaTrader on Windows once the OS itself takes its share; treat VM-1 as the real starting point. And Evoxt's order page has shown the entry plan at $2.99 rather than the $3.49 on the pricing table, so read the total at checkout rather than the marketing figure.

## Choose the city before the plan

A broker's server location, not your home address, decides where your VPS should sit. Broker server information published in October 2026 puts **IC Markets, FP Markets, Axi and Global Prime in Equinix NY4** (New York), **FxPro, Admirals, Darwinex and BlackBull in LD4 or LD5** (London), **FXTM in Frankfurt**, and **Exness in Amsterdam**.

Two things trip people up here. Some brokers run different entities or platforms in different cities, so the London branch of a brand you know may not be the server your account connects to. Brokers also migrate hardware. Confirm before you order, not after.

The check takes a minute inside the terminal you already use. In MT4 or MT5, the login dialog lists every server your broker offers with a ping figure next to each; the bottom-right connection status shows the ping to the one you're on. Whichever server shows the lowest number is the one your VPS should sit near.

What the ping does not tell you is fill quality. A provider can only shorten the wire between your terminal and the broker's gateway; slippage and execution still depend on the venue and on market conditions. Advertised sub-1 ms figures describe the network hop between a datacenter and a broker in the same building, and nothing beyond that.

Evoxt's location list has covered 16 regions, including New York, London, Frankfurt, Amsterdam, Tokyo, Osaka, Hong Kong and Sydney. For FX that gives you the four hubs that matter plus Asia-Pacific coverage for brokers based there. Confirm your specific city on the deploy screen, since the list changes over time. 👉 [Check which Evoxt regions are available](https://bit.ly/EvoXt)

## How much RAM your EA actually needs

Budget 512 MB to 1 GB of RAM per MT4 or MT5 instance, then add headroom for charts and indicators, which consume considerably more than the terminal itself. Translating that into plans:

| Terminals you run | RAM to buy | Evoxt plan | Monthly |
| --- | --- | --- | --- |
| 1–2, few charts each | 2 GB | VM-1 | $5.99 |
| 2–4 with indicators | 4 GB | VM-2 | $11.99 |
| 4–8, or copier plus terminals | 8 GB | VM-4 | $23.99 |
| 8–12 | 16 GB | VM-8 | $47.99 |

Provider guidance lines up with that. MassiveGRID maps 2 GB to one or two terminals, 8 GB to three to eight, and 16 GB to ten or more. ForexVPS sizes its 4 GB tier at one to three trading platforms and its 8 GB tier at six or more. My Forex VPS suggests a 1–3 chart start per terminal and watching Task Manager, adding terminals only while memory and CPU stay under 80%.

The conservative number in that table is the one to buy. An EA that runs fine on a quiet Tuesday can stall when a news release fires and every chart recalculates at once, and the RAM you saved is not worth a missed stop.

## Why a high-clock dual-core beats a many-core server here

MetaTrader 4 and MetaTrader 5 do most of their work on a single thread. They do not spread an EA's calculations evenly across sixteen cores. A 1-core VM running at 6.0 GHz will generally outperform an 8-core VM at 2.5 GHz for a single terminal, which is the reason Evoxt's low-core plans remain usable for this workload and why the plan names emphasise clock speed over core count.

Cores start to matter when you run several terminals in parallel, each with its own thread, or when you add a copier alongside your EAs. That is the jump from VM-1 to VM-2 or VM-3, and it is worth paying for only if you actually run more than one terminal.

## What the forex-specialist premium buys you

The same 4 GB of RAM costs roughly three times as much at a forex-branded host. That gap buys specific things, and whether they matter depends on how much setup you want to do yourself.

| Provider | Entry price worth using | Refund window | What the price covers |
| --- | --- | --- | --- |
| Evoxt | VM-1, $5.99/mo, 2 GB | See current terms | Bare Windows or Linux VM, weekly backups, you install and configure everything |
| ForexVPS | Core, $36/mo promotional ($40 list), 4 GB | 14 days | Preconfigured trading host, DDoS protection, backups, support, broker latency lookup |
| QuantVPS | from $29.99/mo; London Starter+ $39.99 | 14 days | Dedicated CPU and memory, 99.999% monthly availability SLA, New York and London only |
| MassiveGRID | $2.87/mo at 2 GB; Pro from $9.73 with Windows Server licence | 15 days | HA cluster with automatic failover, four cities, Windows licence included on Pro |

The specialist hosts sell convenience as much as hardware: MT4 or MT5 preinstalled, a Windows licence bundled, a support desk that knows what an EA is, and a refund window to test with. If you want to hand over setup and have someone to call during a bad fill, that premium is defensible.

Evoxt's trade is the opposite one. You get more compute per dollar and a much wider spread of locations, and you do the installation yourself: connect over RDP, install MT4 or MT5 from your broker's site, drop your EA files into the terminal's data folder, and set the terminal to relaunch after a reboot through Windows Task Scheduler. If you have installed MetaTrader on a Windows machine before, this is a twenty-minute job. 👉 [Start with a $5.99 Evoxt VM and build the stack yourself](https://bit.ly/EvoXt)

## Two things that make a working VPS look broken

**Disconnecting Remote Desktop is not the same as signing out.** Closing the RDP window leaves your terminals and EAs running on the server. Signing out of Windows, restarting, or shutting the VM down stops them. If your EA "ran overnight and did nothing", check whether something signed the session out rather than assuming the strategy failed.

**A reboot without autostart takes you offline silently.** Windows updates restart servers. Unless the terminal is set to launch on login and the session is configured to stay logged in, the platform comes back to a login screen with no EA attached. Set it up on day one, before you go live.

Evoxt's control panel includes browser-based VNC access, which gets you into the machine when RDP refuses to connect, plus firewall rules, IP reassignment and VM cloning if you want to duplicate a working setup rather than rebuild it.

## Before you pay

Evoxt accepts credit and debit cards, PayPal, Bitcoin and USDt Tron, and bills monthly through to three-year prepay. Start monthly. The discount on a long prepay is not worth committing to before you have confirmed that your broker's server pings well from the region you picked and that your EA runs cleanly through a full session.

Windows is on Evoxt's OS list alongside its Linux images; check the Windows option and its terms on the order page so the total you compare against a forex host is the real one. If refund terms matter to your decision, read them before checkout rather than after.

**The short version.** One or two terminals, broker in New York or London: VM-1 in that same city at $5.99/month. Three to six terminals: VM-2 at $11.99. Eight or more, or a copier farm: VM-4 at $23.99. You want MT4 preinstalled, a bundled Windows licence and a 14-day exit: pay a forex specialist instead, and expect to pay three to eight times as much for the same RAM. 👉 [Deploy the Evoxt plan that matches your terminal count](https://bit.ly/EvoXt)
