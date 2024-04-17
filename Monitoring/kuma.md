docker run -d --restart=always -p 3001:3001 -v uptime-kuma:/app/data --name uptime-kuma louislam/uptime-kuma:1

docker run -d --restart=always -p 192.168.31.55:3001:3001 -v uptime-kuma:/app/data --name uptime-kuma louislam/uptime-kuma:1
-------------------------------------------------------------------------------------


MikroTik PING: 




{
:local avgRtt;
/tool flood-ping 8.8.8.8 count=10 do={
    :if ($sent = 10) do={
        :set avgRtt $"avg-rtt"
    }
}
/tool fetch url="http://192.168.31.55:3001/api/push/R60BLJ3op0?status=up&msg=OK&ping=" mode=http;
}




----------------------------------
PPOE Example:



{
:local InterfaceName "pppoe-out1"

:local InterfaceStat

/interface pppoe-client monitor $InterfaceName once do={
    :set InterfaceStat $status
}

:if ($InterfaceStat = "connected") do={
    
    /tool fetch url="http://192.168.31.55:3001/api/push/Pjf3VN17Lx?status=up&msg=OK&ping=" mode=http;

} else={
    :log warning "PPPoE service is not connected. Status: $InterfaceStat"
}
}

--------------------------------------
L2tp Example:


{
:local InterfaceName "l2tp-out1"


:local InterfaceStat

/interface l2tp-client monitor $InterfaceName once do={
    :set InterfaceStat $status
}

:if ($InterfaceStat = "connected") do={
    # Your "up" code goes here
    /tool fetch url="http://192.168.31.55:3001/api/push/7IV6V5rxW8?status=up&msg=OK&ping=" mode=http;
} else={
    :log warning "L2TP service is not connected. Status: $InterfaceStat"
}
}
