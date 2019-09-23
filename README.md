# Zlinux
#Add a json for zlinux

#I couldnt find the information about zlinux in the last package. In the linux json file didnt have the parameters for uptime.
#Added this information in the file. 



{
        "os_settings": {
                "disksCommand": "",
                "disksRegex": "",
                "interfacesCommand": "/sbin/ip link show",
                "interfacesRegex": "\\d+:\\s+(\\w+\\d*):.*",
                "pageSizeCommand": "/usr/bin/getconf PAGESIZE"
        },
        "commands": [{
                        "eventType": "DiskSpace",
                        "command": "df -Pk -x iso9660 -x cdfs -x hsfs",
                        "checkAllRegex": false,
                        "lineLimit": 0,
                        "mappings": [{
                                "expression": "\\s*(\\S+)\\s+(\\d+)\\s+(\\d+)\\s+(\\d+)\\s+(\\d+)[%]\\s+(\\S+)",
                                "metrics": [{
                                                "name": "DISK_NAME"
                                        },
                                        {
                                                "name": "Total",
                                                "ratio": 1,
                                                "type": "NORMAL"
                                        },
                                        {
                                                "name": "Used",
                                                "ratio": 1,
                                                "type": "NORMAL"
                                        },
                                        {
                                                "name": "Free",
                                                "ratio": 1,
                                                "type": "NORMAL"
                                        },
                                        {
                                                "name": "Percent Used",
                                                "ratio": 1,
                                                "type": "NORMAL"
                                        },
                                        {
                                                "name": "Mount Point",
                                                "type": "ATTRIBUTE"
                                        }
                                ]
                        }]
                },
                {
                        "eventType": "DiskInodes",
                        "command": "df -Pi -x iso9660 -x cdfs -x hsfs",
                        "checkAllRegex": false,
                        "lineLimit": 0,
                        "mappings": [{
                                "expression": "\\s*(\\S+)\\s+(\\d+)\\s+(\\d+)\\s+(\\d+)\\s+(\\d+)[%]\\s+(\\S+)",
                                "metrics": [{
                                        "name": "DISK_NAME"
                                },
                                        {
                                                "name": "Total",
                                                "ratio": 1,
                                                "type": "NORMAL"
                                        },
                                        {
                                                "name": "Used",
                                                "ratio": 1,
                                                "type": "NORMAL"
                                        },
                                        {
                                                "name": "Free",
                                                "ratio": 1,
                                                "type": "NORMAL"
                                        },
                                        {
                                                "name": "Percent Used",
                                                "ratio": 1,
                                                "type": "NORMAL"
                                        },
                                        {
                                                "name": "Mount Point",
                                                "type": "ATTRIBUTE"
                                        }
                                ]
                        }]
                },
                {
                        "eventType": "DiskIO",
                        "command": "cat /proc/diskstats",
                        "checkAllRegex": false,
                        "lineLimit": 0,
                        "mappings": [{
                                "expression": "\\d+\\s+\\d+\\s+(\\S+)\\s+(\\d+)\\s+(\\d+)\\s+(\\d+)\\s+(\\d+)\\s+(\\d+)\\s+(\\d+)\\s+(\\d+)\\s+(\\d+)\\s+(\\d+)\\s+(\\d+)\\s+(\\d+)",
                                "metrics": [{
                                                "name": "METRIC_PREFIX"
                                        },
                                        {
                                                "name": "Reads Per Interval",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "name": "Reads Merged Per Interval",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "name": "Sectors Read Per Interval",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "name": "Time Spent Reading",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "name": "Writes Per Interval",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "name": "Writes Merged Per Interval",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "name": "Sectors Per Interval",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "name": "Time Spent Writing",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "name": "IO In progress",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "name": "Time Spent on IO",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "name": "Time Spent on IO (Weighted)",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        }
                                ]
                        }]
                },
                {
                        "eventType": "NetworkIO",
                        "command": "grep -r . /sys/class/net/MEMBER_PLACEHOLDER/statistics 2>&1",
                        "checkAllRegex": false,
                        "lineLimit": 0,
                        "mappings": [{
                                "expression": "\\/sys\\/class\\/net\\/[\\w\\d]+\\/statistics\\/([\\w_]+):(\\d+)",
                                "metrics": [{
                                                "name": "METRIC_NAME"
                                        },
                                        {
                                                "name": "METRIC_VALUE"
                                        }
                                ],
                                "translations": [{
                                                "input": "collisions",
                                                "output": "Collisions",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "multicast",
                                                "output": "Multicast",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "rx_bytes",
                                                "output": "Receive.Bytes",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "rx_compressed",
                                                "output": "Receive.Compressed",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "rx_crc_errors",
                                                "output": "Receive.CRC Errors",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "rx_dropped",
                                                "output": "Receive.Dropped",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "rx_errors",
                                                "output": "Receive.Errors",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "rx_fifo_errors",
                                                "output": "Receive.FIFO Errors",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "rx_frame_errors",
                                                "output": "Receive.Frame Errors",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "rx_length_errors",
                                                "output": "Receive.Length Errors",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "rx_missed_errors",
                                                "output": "Receive.Missed Errors",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "rx_over_errors",
                                                "output": "Receive.Overrun Errors",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "rx_packets",
                                                "output": "Receive.Packets",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "tx_aborted_errors",
                                                "output": "Transmit.Aborted Errors",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "tx_bytes",
                                                "output": "Transmit.Bytes",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "tx_carrier_errors",
                                                "output": "Transmit.Carrier Errors",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "tx_compressed",
                                                "output": "Transmit.Compressed",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "tx_dropped",
                                                "output": "Transmit.Dropped",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "tx_errors",
                                                "output": "Transmit.Errors",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "tx_fifo_errors",
                                                "output": "Transmit.FIFO Errors",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "tx_heartbeat_errors",
                                                "output": "Transmit.Heartbeat Errors",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "tx_packets",
                                                "output": "Transmit.Packets",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        },
                                        {
                                                "input": "tx_window_errors",
                                                "output": "Transmit.Window Errors",
                                                "ratio": 1,
                                                "type": "DELTA"
                                        }
                                ]
                        }]
                },
                {
                        "eventType": "Process",
                        "command": "ps -ewwo pid,state,%cpu,%mem,rss,vsz,euser,command",
                        "checkAllRegex": false,
                        "lineLimit": 0,
                        "mappings": [{
                                "expression": "(\\d+)\\s+([A-Z]{1})\\s+([0-9\\.]+)\\s+([0-9\\.]+)\\s+(\\d+)\\s+(\\d+)\\s+(\\S+)\\s+(.*)",
                                "metrics": [{
                                                "name": "PID",
                                                "type": "ATTRIBUTE"
                                        },
                                        {
                                                "name": "State",
                                                "type": "ATTRIBUTE"
                                        },
                                        {
                                                "name": "CPU",
                                                "ratio": 1,
                                                "type": "NORMAL"
                                        },
                                        {
                                                "name": "Memory",
                                                "ratio": 1,
                                                "type": "NORMAL"
                                        },
                                        {
                                                "name": "Resident Set Size",
                                                "ratio": 1,
                                                "type": "NORMAL"
                                        },
                                        {
                                                "name": "Virtual Size",
                                                "ratio": 1,
                                                "type": "NORMAL"
                                        },
                                        {
                                                "name": "User",
                                                "type": "ATTRIBUTE"
                                        },
                                        {
                                                "name": "PROCESS_NAME"
                                        }
                                ]
                        }]
                },
                {
                        "eventType": "Stats",
                        "command": "top -bH -n 2",
                        "checkAllRegex": false,
                        "lineLimit": 5,
                        "mappings": [
                                {
                                        "expression": ".*Mem:\\s+(\\d+)k\\s+total,\\s+(\\d+)k\\s+used,\\s+(\\d+)k\\s+free,\\s+(\\d+)k\\s+buff.*",
                                        "metrics": [{
                                                        "name": "Memory.Total",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "Memory.Used",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "Memory.Free",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "Memory.Buffer",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                }
                                        ]
                                },
                                {
                                        "expression": "KiB Mem\\s*:\\s+(\\d+)\\s+total,\\s+(\\d+)\\s+used,\\s+(\\d+)\\s+free,\\s+(\\d+)\\s+buff.*",
                                        "metrics": [{
                                                        "name": "Memory.Total",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "Memory.Used",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "Memory.Free",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "Memory.Buffer",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                }
                                        ]
                                },
                                {
                                        "expression": "KiB Mem\\s*:\\s+(\\d+)\\s+total,\\s+(\\d+)\\s+free,\\s+(\\d+)\\s+used,\\s+(\\d+)\\s+buff.*",
                                        "metrics": [{
                                                        "name": "Memory.Total",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "Memory.Free",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "Memory.Used",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "Memory.Buffer",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                }
                                        ]
                                },
                                {
                                        "expression": ".*Swap:\\s+(\\d+)k\\s+total,\\s+(\\d+)k\\s+used,\\s+(\\d+)k\\s+free,\\s+(\\d+)k\\s+cached",
                                        "metrics": [{
                                                        "name": "Swap.Total",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "Swap.Used",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "Swap.Free",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "Swap.Buffer",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                }
                                        ]
                                },
                                {
                                        "expression": "KiB Swap:\\s+(\\d+)\\s+total,\\s+(\\d+)\\s+used,\\s+(\\d+)\\s+free,\\s+(\\d+)\\s+cached",
                                        "metrics": [{
                                                        "name": "Swap.Total",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "Swap.Used",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "Swap.Free",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "Swap.Buffer",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                }
                                        ]
                                },
                                {
                                        "expression": "KiB Swap:\\s+(\\d+)\\s+total,\\s+(\\d+)\\s+free,\\s+(\\d+)\\s+used[,\\.]*\\s+(\\d+)\\s+avail.*",
                                        "metrics": [{
                                                        "name": "Swap.Total",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "Swap.Free",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "Swap.Used",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "Swap.Available",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                }
                                        ]
                                },
                                {
                                        "expression": "Threads:\\s+(\\d+)\\s+total,\\s+(\\d+)\\s+running,\\s+(\\d+)\\s+sleeping,\\s+(\\d+)\\s+stopped,\\s+(\\d+)\\s+zombie",
                                        "metrics": [{
                                                        "name": "KernelThreads.Total",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "KernelThreads.Runnable",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "KernelThreads.Sleeping",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "KernelThreads.Stopped",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "KernelThreads.Zombie",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                }
                                        ]
                                },
                                {
                                        "expression": "[%]*Cpu[^:]*:\\s+([\\d\\.]+)[%]*\\s*us,\\s+([\\d\\.]+)[%]*\\s*sy,\\s+([\\d\\.]+)[%]*\\s*ni,\\s+([\\d\\.]+)[%]*\\s*id,\\s+([\\d\\.]+)[%]*\\s*wa,\\s+([\\d\\.]+)[%]*\\s*hi,\\s+([\\d\\.]+)[%]*\\s*si,\\s+([\\d\\.]+)[%]*\\s*st",
                                        "metrics": [{
                                                        "name": "CPU.User",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "CPU.System",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "CPU.Nice",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "CPU.Idle",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "CPU.Waiting",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "CPU.Interrupt-Hardware",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "CPU.Interrupt-Software",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "CPU.Stolen",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                }
                                        ]
                                },
                                {
                                        "expression": "top.+up (\\d+:\\d+).+load average:\\s+([0-9\\.]+),\\s+([0-9\\.]+),\\s+([0-9\\.]+)",
                                        "metrics": [{
                                                        "name": "Up Time",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },{
                                                        "name": "LoadAverage.1 Minute",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "LoadAverage.5 Minute",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "LoadAverage.15 Minute",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                }
                                        ]
                                }
                        ]
                },
                {
                        "eventType": "Stats",
                        "command": "uptime",
                        "checkAllRegex": false,
                        "lineLimit": 0,
                        "interval":     0,
                        "mappings": [
                                {
                                        "expression": ".*up\\s+([0-9\\s+a-z]+).*load average:\\s+([0-9\\.]+),\\s+([0-9\\.]+),\\s+([0-9\\.]+)",
                                        "metrics": [
                                                {
                                                        "name": "Uptime",
                                                        "type": "ATTRIBUTE"
                                                },
                                                {
                                                        "name": "LoadAverage.1 Minute",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "LoadAverage.5 Minute",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "LoadAverage.15 Minute",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                }
                                        ]
                                }
                        ]
                },
                {
                        "eventType": "Vmstat",
                        "command": "vmstat -s",
                        "checkAllRegex": false,
                        "lineLimit": 0,
                        "mappings": [{
                                        "expression": "\\s*(\\d+)\\s+(?!K\\s+)(.+)(?=ticks)",
                                        "metrics": [{
                                                        "name": "METRIC_VALUE",
                                                        "ratio": 1,
                                                        "type": "DELTA"
                                                },
                                                {
                                                        "name": "METRIC_NAME"
                                                }
                                        ]
                                },
                                {
                                        "expression": "\\s*(\\d+)\\s+(?!K\\s+)(.+)",
                                        "metrics": [{
                                                        "name": "METRIC_VALUE",
                                                        "ratio": 1,
                                                        "type": "DELTA"
                                                },
                                                {
                                                        "name": "METRIC_NAME"
                                                }
                                        ]
                                },
                                {
                                        "expression": "\\s*(\\d+)\\s+K\\s+(.+)",
                                        "metrics": [{
                                                        "name": "METRIC_VALUE",
                                                        "ratio": 1,
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "METRIC_NAME"
                                                }
                                        ]
                                }
                        ]
                },
                {
                        "eventType": "MissingProcFiles",
                        "command": "sh find-missing-procfiles.sh",
                        "checkAllRegex": false,
                        "lineLimit": 0,
                        "mappings": [
                                {
                                        "expression": "(\\S+):(\\d+),.+ (\\S+): No such file or directory",
                                        "metrics": [{
                                                        "name": "METRIC_PREFIX"
                                                },
                                                {
                                                        "name": "PID",
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "File",
                                                        "type": "NORMAL"
                                                }
                                        ]
                                },
                                {
                                        "expression": "(\\S+):(\\d?),.+ (\\S+)",
                                        "metrics": [{
                                                        "name": "METRIC_PREFIX"
                                                },
                                                {
                                                        "name": "PID",
                                                        "type": "NORMAL"
                                                },
                                                {
                                                        "name": "File",
                                                        "type": "NORMAL"
                                                }
                                        ]
                                }
                        ]
                }
        ]
}
