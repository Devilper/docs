### 通过元类创建`ORM`

~~~python
# 创建一个Field类
class Field(object):
    def __init__(self, name, column_type):
        self.name = name
        self.column_type = column_type

    def __str__(self):
        return f'<{self.__class__.__name__}:{self.name}>'


# 创建StringField和IntegerField
class StringField(Field):

    def __init__(self, name):
        super(StringField, self).__init__(name, 'varchar(100)')


class IntegerField(Field):
    def __init__(self, name):
        super(IntegerField, self).__init__(name, 'bigint')


# 道生一
class ModelMetaclass(type):
    def __new__(cls, name, bases, attrs):
        if name == 'Model':
            return type.__new__(cls, name, bases, attrs)
        print(f'Found model:{name}')

        # 创建一个新字典mapping
        mappings = dict()

        # 将每一个类的属性，通过.items()遍历其键值对、如果值是Field类，则打印键值，并将这一对键值绑定到mapping字典上
        for k, v in attrs.items():
            if isinstance(v, Field):
                print(f'Found mapping:{k} ==>{v}')
                mappings[k] = v
        # 将刚刚传入值为Field类的属性删除
        for k in mappings.keys():
            attrs.pop(k)

        # 创建一个专门的mappings属性，保存字典mapping
        attrs['__mappings__'] = mappings  # 保存属性和列的映射关系

        # 创建一个专门的table属性，保存传入的类的名称
        attrs['__table__'] = name  # 假设表名和类名一致
        return type.__new__(cls, name, bases, attrs)


# 一生二
class Model(dict, metaclass=ModelMetaclass):
    def __init__(self, **kwargs):
        super(Model, self).__init__(**kwargs)

    def __getattr__(self, key):
        try:
            print(self)
            return self[key]
        except KeyError:
            raise AttributeError(f"'Model object has not attribute '{key}'")

    def __setattr__(self, key, value):
        self[key] = value

    # 模拟建表操作
    def save(self):
        fields = []
        args = []
        print(self.__mappings__)
        for k, v in self.__mappings__.items():
            fields.append(v.name)
            args.append(getattr(self, k))

        sql = f"insert into {self.__table__}({','.join(fields)}) values({','.join([str(i) for i in args])})"

        print(f'SQL:{sql}')
        print(f'ARGS:{str(args)}')


# 创建一个子类User
class User(Model):
    # 定义类的属性到列的映射
    id = IntegerField('id')
    name = StringField('username')
    email = StringField('email')
    password = StringField('password')


# 初始化实例并调用save
u = User(id=123456, name='Batman', email='ba@da.org', password='iamback')
u.save()

~~~

