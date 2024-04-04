# Danh sách metrics của Host

### Linux OS

| **Linux Metric**       | **Metric (Tên metric)**                                                                | **Unit (Đơn vị tính), Loại OS hỗ trợ**                            | **Mô tả** |
| ---------------------- | -------------------------------------------------------------------------------------- | ----------------------------------------------------------------- | --------- |
| CPU (22 metrics)       | Prefix sẽ là cpu.\<tên\_metric>, tên metric bao gồm:                                   |                                                                   |           |
| time\_user             | float                                                                                  | N/A                                                               |           |
| time\_system           | float                                                                                  | N/A                                                               |           |
| time\_idle             | float                                                                                  | N/A                                                               |           |
| time\_active           | float                                                                                  | N/A                                                               |           |
| time\_nice             | float                                                                                  | N/A                                                               |           |
| time\_iowait           | float                                                                                  | N/A                                                               |           |
| time\_irq              | float                                                                                  | N/A                                                               |           |
| time\_softirq          | float                                                                                  | N/A                                                               |           |
| time\_steal            | float                                                                                  | N/A                                                               |           |
| time\_guest            | float                                                                                  | N/A                                                               |           |
| time\_guest\_nice      | float                                                                                  | N/A                                                               |           |
| usage\_user            | float, percent                                                                         | N/A                                                               |           |
| usage\_system          | float, percent                                                                         | N/A                                                               |           |
| usage\_idle            | float, percent                                                                         | N/A                                                               |           |
| usage\_active          | float                                                                                  | N/A                                                               |           |
| usage\_nice            | float, percent                                                                         | N/A                                                               |           |
| usage\_iowait          | float, percent                                                                         | N/A                                                               |           |
| usage\_irq             | float, percent                                                                         | N/A                                                               |           |
| usage\_softirq         | float, percent                                                                         | N/A                                                               |           |
| usage\_steal           | float, percent                                                                         | N/A                                                               |           |
| usage\_guest           | float, percent                                                                         | N/A                                                               |           |
| usage\_guest\_nice     | float, percent                                                                         | N/A                                                               |           |
| DISK (7 metrics)       | Prefix sẽ có dạng disk.\<tên\_metric>, tên metric sẽ bao gồm:                          |                                                                   |           |
| free                   | integer, bytes                                                                         | N/A                                                               |           |
| total                  | integer, bytes                                                                         | N/A                                                               |           |
| used                   | integer, bytes                                                                         | N/A                                                               |           |
| used\_percent          | float, percent                                                                         | N/A                                                               |           |
| inodes\_free           | integer, files                                                                         | N/A                                                               |           |
| inodes\_total          | integer, files                                                                         | N/A                                                               |           |
| inodes\_used           | integer, files                                                                         | N/A                                                               |           |
| DISKIO (11 metrics)    | Prefix sẽ có dạng diskio.\<tên\_metric>, tên metric sẽ bao gồm:                        |                                                                   |           |
| reads                  | integer, counter                                                                       | N/A                                                               |           |
| writes                 | integer, counter                                                                       | N/A                                                               |           |
| read\_bytes            | integer, counter, bytes                                                                | N/A                                                               |           |
| write\_bytes           | integer, counter, bytes                                                                | N/A                                                               |           |
| read\_time             | integer, counter, milliseconds                                                         | N/A                                                               |           |
| write\_time            | integer, counter, milliseconds                                                         | N/A                                                               |           |
| io\_time               | integer, counter, milliseconds                                                         | N/A                                                               |           |
| weighted\_io\_time     | integer, counter, milliseconds                                                         | N/A                                                               |           |
| iops\_in\_progress     | integer, gauge                                                                         | N/A                                                               |           |
| merged\_reads          | integer, counter                                                                       | N/A                                                               |           |
| merged\_writes         | integer, counter                                                                       | N/A                                                               |           |
| KERNEL (7 metrics)     | Prefix sẽ có dạng kernel.\<tên\_metric>, tên metric và dimension tương ứng sẽ bao gồm: |                                                                   |           |
| boot\_time             | integer, seconds since epoch, btime                                                    | N/A                                                               |           |
| context\_switches      | integer, ctxt                                                                          | N/A                                                               |           |
| disk\_pages\_in        | integer, page                                                                          | N/A                                                               |           |
| disk\_pages\_out       | integer, page                                                                          | N/A                                                               |           |
| interrupts             | integer, intr                                                                          | N/A                                                               |           |
| processes\_forked      | integer, processes                                                                     | N/A                                                               |           |
| entropy\_avail         | integer, entropy\_available                                                            | N/A                                                               |           |
| MEM (34 metrics)       | Prefix sẽ có dạng mem.\<tên\_metric>, tên metric tương ứng loại OS hỗ trợ sẽ bao gồm:  |                                                                   |           |
| active                 | integer, Darwin, FreeBSD, Linux, OpenBSD                                               | N/A                                                               |           |
| available              | integer                                                                                | N/A                                                               |           |
| available\_percent     | float                                                                                  | N/A                                                               |           |
| buffered               | integer, FreeBSD, Linux                                                                | N/A                                                               |           |
| cached                 | integer, FreeBSD, Linux, OpenBSD                                                       | N/A                                                               |           |
| commit\_limit          | integer, Linux                                                                         | N/A                                                               |           |
| committed\_as          | integer, Linux                                                                         | N/A                                                               |           |
| dirty                  | integer, Linux                                                                         | N/A                                                               |           |
| free                   | integer, Darwin, FreeBSD, Linux, OpenBSD                                               | N/A                                                               |           |
| high\_free             | integer, Linux                                                                         | N/A                                                               |           |
| high\_total            | integer, Linux                                                                         | N/A                                                               |           |
| huge\_pages\_free      | integer, Linux                                                                         | N/A                                                               |           |
| huge\_page\_size       | integer, Linux                                                                         | N/A                                                               |           |
| huge\_pages\_total     | integer, Linux                                                                         | N/A                                                               |           |
| inactive               | integer, Darwin, FreeBSD, Linux, OpenBSD                                               | N/A                                                               |           |
| laundry                | integer, FreeBSD                                                                       | N/A                                                               |           |
| low\_free              | integer, Linux                                                                         | N/A                                                               |           |
| low\_total             | integer, Linux                                                                         | N/A                                                               |           |
| mapped                 | integer, Linux                                                                         | N/A                                                               |           |
| page\_tables           | integer, Linux                                                                         | N/A                                                               |           |
| shared                 | integer, Linux                                                                         | N/A                                                               |           |
| slab                   | integer, Linux                                                                         | N/A                                                               |           |
| sreclaimable           | integer, Linux                                                                         | N/A                                                               |           |
| sunreclaim             | integer, Linux                                                                         | N/A                                                               |           |
| swap\_cached           | integer, Linux                                                                         | N/A                                                               |           |
| swap\_free             | integer, Linux                                                                         | N/A                                                               |           |
| swap\_total            | integer, Linux                                                                         | N/A                                                               |           |
| total                  | integer                                                                                | N/A                                                               |           |
| used                   | integer                                                                                | N/A                                                               |           |
| used\_percent          | float                                                                                  | N/A                                                               |           |
| vmalloc\_chunk         | integer, Linux                                                                         | N/A                                                               |           |
| vmalloc\_total         | integer, Linux                                                                         | N/A                                                               |           |
| vmalloc\_used          | integer, Linux                                                                         | N/A                                                               |           |
| wired                  | integer, Darwin, FreeBSD, OpenBSD                                                      | N/A                                                               |           |
| write\_back            | integer, Linux                                                                         | N/A                                                               |           |
| write\_back\_tmp       | integer, Linux                                                                         | N/A                                                               |           |
| PROCESSES (11 metrics) | Prefix sẽ có dạng processes.\<tên\_metric>, tên metric kèm loại OS hỗ trợ sẽ bao gồm   |                                                                   |           |
| blocked                | aka disk sleep or uninterruptible sleep                                                | N/A                                                               |           |
| running                | N/A                                                                                    | N/A                                                               |           |
| sleeping               | N/A                                                                                    | N/A                                                               |           |
| stopped                | N/A                                                                                    | N/A                                                               |           |
| total                  | N/A                                                                                    | N/A                                                               |           |
| zombie                 | N/A                                                                                    | N/A                                                               |           |
| dead                   | N/A                                                                                    | N/A                                                               |           |
| wait                   | freebsd only                                                                           | N/A                                                               |           |
| idle                   | bsd and Linux 4+ only                                                                  | N/A                                                               |           |
| paging                 | linux only                                                                             | N/A                                                               |           |
| parked                 | linux only                                                                             | N/A                                                               |           |
| total\_threads         | linux only                                                                             | N/A                                                               |           |
| SWAP (6 metrics)       | Prefix sẽ có dạng swap.\<tên\_metric>, tên metric sẽ bao gồm:                          |                                                                   |           |
| free                   | int, bytes                                                                             |  Free swap memory                                                 |           |
| total                  | int, bytes                                                                             |  Total swap memory                                                |           |
| used                   | int, bytes                                                                             |  Used swap memory                                                 |           |
| used\_percent          | float, percent                                                                         |  Percentage of swap memory used                                   |           |
| in                     | int, bytes                                                                             |  Data swapped in since last boot calculated from page number      |           |
| out                    | int, bytes                                                                             |  Data swapped out since last boot calculated from page number     |           |
| SYSTEM (7 metrics)     | Prefix sẽ có dạng system.\<tên\_metric>, tên metric sẽ bao gồm:                        |                                                                   |           |
| load1                  | float                                                                                  | N/A                                                               |           |
| load15                 | float                                                                                  | N/A                                                               |           |
| load5                  | float                                                                                  | N/A                                                               |           |
| n\_users               | integer                                                                                | N/A                                                               |           |
| n\_cpus                | integer                                                                                | N/A                                                               |           |
| uptime                 | integer, seconds                                                                       | N/A                                                               |           |
| uptime\_format         | string, deprecated in 1.10, use uptime field                                           | N/A                                                               |           |
| NET (8 metrics)        | Prefix sẽ có dạng net.\<tên\_metric>, tên metric sẽ bao gồm:                           |                                                                   |           |
| bytes\_sent            | N/A                                                                                    |  The total number of bytes sent by the interface                  |           |
| bytes\_recv            | N/A                                                                                    |  The total number of bytes received by the interface              |           |
| packets\_sent          | N/A                                                                                    |  The total number of packets sent by the interface                |           |
| packets\_recv          | N/A                                                                                    |  The total number of packets received by the interface            |           |
| err\_in                | N/A                                                                                    |  The total number of receive errors detected by the interface     |           |
| err\_out               | N/A                                                                                    |  The total number of transmit errors detected by the interface    |           |
| drop\_in               | N/A                                                                                    |  The total number of received packets dropped by the interface    |           |
| drop\_out              | N/A                                                                                    |  The total number of transmitted packets dropped by the interface |           |

***

### Windows OS

| **Window Metric**                                | **Metric (Tên metric)**                                              |
| ------------------------------------------------ | -------------------------------------------------------------------- |
| Processor                                        | Prefix sẽ có dạng win\_cpu.\<tên\_metric>, tên metric sẽ bao gồm:    |
| win\_cpu.Percent\_DPC\_Time                      |                                                                      |
| win\_cpu.Percent\_Idle\_Time                     |                                                                      |
| win\_cpu.Percent\_Interrupt\_Time                |                                                                      |
| win\_cpu.Percent\_Privileged\_Time               |                                                                      |
| win\_cpu.Percent\_Processor\_Time                |                                                                      |
| win\_cpu.Percent\_User\_Time                     |                                                                      |
| Win\_Disk                                        | Prefix sẽ có dạng win\_disk.\<tên\_metric>, tên metric sẽ bao gồm:   |
| win\_disk.Current\_Disk\_Queue\_Length           |                                                                      |
| win\_disk.Free\_Megabytes                        |                                                                      |
| win\_disk.Percent\_Disk\_Read\_Time              |                                                                      |
| win\_disk.Percent\_Disk\_Time                    |                                                                      |
| win\_disk.Percent\_Disk\_Write\_Time             |                                                                      |
| win\_disk.Percent\_Free\_Space                   |                                                                      |
| win\_disk.Percent\_Idle\_Time                    |                                                                      |
| Win\_DiskIO                                      | Prefix sẽ có dạng win\_diskio.\<tên\_metric>, tên metric sẽ bao gồm: |
| win\_diskio.Current\_Disk\_Queue\_Length         |                                                                      |
| win\_diskio.Disk\_Read\_Bytes\_persec            |                                                                      |
| win\_diskio.Disk\_Reads\_persec                  |                                                                      |
| win\_diskio.Disk\_Write\_Bytes\_persec           |                                                                      |
| win\_diskio.Disk\_Writes\_persec                 |                                                                      |
| win\_diskio.Percent\_Disk\_Read\_Time            |                                                                      |
| win\_diskio.Percent\_Disk\_Time                  |                                                                      |
| win\_diskio.Percent\_Disk\_Write\_Time           |                                                                      |
| Network Interface                                | Prefix sẽ có dạng win\_net.\<tên\_metric>, tên metric sẽ bao gồm:    |
| win\_net.Bytes\_Received\_persec                 |                                                                      |
| win\_net.Bytes\_Sent\_persec                     |                                                                      |
| win\_net.Packets\_Outbound\_Discarded            |                                                                      |
| win\_net.Packets\_Outbound\_Errors               |                                                                      |
| win\_net.Packets\_Received\_Discarded            |                                                                      |
| win\_net.Packets\_Received\_Errors               |                                                                      |
| win\_net.Packets\_Received\_persec               |                                                                      |
| win\_net.Packets\_Sent\_persec                   |                                                                      |
| System                                           | Prefix sẽ có dạng win\_system.\<tên\_metric>, tên metric sẽ bao gồm: |
| win\_system.Context\_Switches\_persec            |                                                                      |
| win\_system.Processor\_Queue\_Length             |                                                                      |
| win\_system.System\_Calls\_persec                |                                                                      |
| win\_system.System\_Up\_Time                     |                                                                      |
| Memory                                           | Prefix sẽ có dạng win\_mem.\<tên\_metric>, tên metric sẽ bao gồm:    |
| win\_mem.Available\_Bytes                        |                                                                      |
| win\_mem.Cache\_Faults\_persec                   |                                                                      |
| win\_mem.Demand\_Zero\_Faults\_persec            |                                                                      |
| win\_mem.Page\_Faults\_persec                    |                                                                      |
| win\_mem.Pages\_persec                           |                                                                      |
| win\_mem.Pool\_Nonpaged\_Bytes                   |                                                                      |
| win\_mem.Pool\_Paged\_Bytes                      |                                                                      |
| win\_mem.Standby\_Cache\_Core\_Bytes             |                                                                      |
| win\_mem.Standby\_Cache\_Normal\_Priority\_Bytes |                                                                      |
| win\_mem.Standby\_Cache\_Reserve\_Bytes          |                                                                      |
| Paging File                                      | Prefix sẽ có dạng win\_swap.\<tên\_metric>, tên metric sẽ bao gồm:   |
| win\_swap.Percent\_Usage                         |                                                                      |

\
