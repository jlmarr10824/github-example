curl -GET http://$QXDB_ES_SERVER:9200/_cat/indices?v 2>/tmp/curl.err >/tmp/curl.dat
if [ $? -eq 0 ];then
	case $(uname) in
	Darwin)
		sort --key=3 /tmp/curl.dat
		;;
	Linux)
		sort -k3 /tmp/curl.dat
		;;
	*)
		print -u2 Unknown platform $(uname)
	esac
else
	cat /tmp/curl.err
fi
