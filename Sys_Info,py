import platform
from datetime import datetime, UTC
import psutil
import time

def get_size(bytes, suffix="B"):
    factor = 1024
    for unit in ["", "K", "M", "G", "T", "P"]:
        if bytes < factor:
            return f"{bytes:.2f}{unit}{suffix}"
        bytes /= factor

def Intro():
    
    print(' ' * 8 + "\033[93mSystem Information\033[0m\n")
    uname = platform.uname()
    print(f"System: {uname.system}\n" 
          f"Model Name: {uname.node}\n" 
          f"Release: {uname.release}\n"  
          f"Version: {uname.version}\n" 
          f"Machine: {uname.machine}\n"  
          f"Processor: {uname.processor}")
    
    print(' ' * 8 + "\033[93mCPU Information\033[0m\n")
    cpu_physical_core = psutil.cpu_count(logical=False)
    total_core_cpu = psutil.cpu_count(logical=True)
    cpu_use = psutil.cpu_percent(percpu=False,interval=1)
    print(f"CPU has {cpu_physical_core} physical cores\n" 
          f"Total cores: {total_core_cpu}\n"
          f"CPU Use: {cpu_use}%")
    
    cpufreq = psutil.cpu_freq()
    print(f"Max Frequency: {cpufreq.max:.2f}Mhz\n"
          f"Min Frequency: {cpufreq.min:.2f}Mhz") 

    print(' ' * 8 + "\033[93mMemory Information\033[0m\n")
    svmem = psutil.virtual_memory()
    swmem = psutil.swap_memory()
    print(f"Total Memory: {get_size(svmem.total)}\n"
          f"Used: {get_size(svmem.used)}\n"
          f"TOtal Swap Memory: {get_size(swmem.total)}\n"
          f"Used: {get_size(swmem.used)}")
    hdd = psutil.disk_usage('/') 
    #print("The CPU usage per core is displayed here:")
    for i, percentage in enumerate(psutil.cpu_percent(percpu=True, interval=1)):
        #print(f"Core {i}: {percentage}%")
    
        print(f"Total CPU Usage: {psutil.cpu_percent()}%")

    drives = ['C', 'D', 'E']
    output_string = ""
    max_drive_length = max(len(drive) for drive in drives)
    for drive_letter in drives:
     drive = psutil.disk_usage(f'{drive_letter}:\\')
     drive_usage_percent = (drive.used / drive.total) * 100
     drive_usage_percent = round(drive_usage_percent, 2)

     output_string += f"{drive_letter}{' ' * (max_drive_length - len(drive_letter))}: {drive_usage_percent}%\n"

    print(output_string)

    print(' ' * 8 + "\033[93mDisk Information\033[0m\n")
    disk_partitions = psutil.disk_partitions(all=False)
    disk_usage = psutil.disk_usage(disk_partitions[0].device)
    disk_io = psutil.disk_io_counters(perdisk=False)
    print(f"Disk Partition: {disk_partitions}")
    print(f"Disk Use: {disk_usage}")
    print(f"Disk I/O Counters: {disk_io}")
    
    print(' ' * 8 + "\033[93mNetwork Information\033[0m\n")
    net_io = psutil.net_io_counters(pernic=False)
    net_connections = psutil.net_connections(kind='inet')
    net_if_addrs = psutil.net_if_addrs()
    net_if_stats = psutil.net_if_stats()
    print(f"Network I/O Counters: {net_io}")
    #print(f"Network Connections: {net_connections}")
    #print(f"Network Interface Addresses: {net_if_addrs}")
    #print(f"Network Interface States: {net_if_stats}")

    print(' ' * 8 + "\033[93mBoot Time\033[0m\n")
    boot_time = psutil.boot_time()
    boot_time = datetime.fromtimestamp(boot_time, UTC)
    formatted_boot_time = boot_time.strftime('%Y-%m-%d %H:%M:%S UTC')
    print(f"System Boot Time: {formatted_boot_time}")

    print(' ' * 8 + "\033[93mConnected Users\033[0m\n")
    users = psutil.users()
    print(f"Connected Users: {users}")

    print(' ' * 8 + "\033[93mProcesses\033[0m\n")
    processes = list(psutil.process_iter())

    print(f"Number of Processes: {len(processes)}")
    #print(f"Process IDs: {[process.pid for process in processes]}")

def live(bars=50, sleep_time=0.5):
    while True:
        cpu_usage = psutil.cpu_percent(interval=1)
        mem_usage = psutil.virtual_memory().percent

        block = "\u2588"  # Unicode for '█' 2588
        empty = "-"       # Placeholder for unused space

        cpu_bar = block * max(1, int((cpu_usage / 100) * bars)) + empty * (bars - max(1, int((cpu_usage / 100) * bars)))
        mem_bar = block * max(1, int((mem_usage / 100) * bars)) + empty * (bars - max(1, int((mem_usage / 100) * bars)))

        print(f"\rCPU: |{cpu_bar}| {cpu_usage:.2f}%   MEMORY: |{mem_bar}| {mem_usage:.2f}% ", end="\r")

        time.sleep(sleep_time)

//live(bars=50)
//Intro()
