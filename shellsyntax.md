echo -e(支持转义符) ""

read -p(打印字符串) "" var(变量)

if [ 条件 ]; then
elif [ 条件 ]; then
else
fi

case $var in
        value1)
                语句
                ;;
        value2)
                语句
                ;;
        *)
                语句
                ;;
esac

while [ 条件 ]
do
done

until [ 条件 ]
do
done

for var in vars
do
done

function fun() {
        语句
}
