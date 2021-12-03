## Installation

    pip3 install ast-magic

To manually load, run the following in your IPython prompt:
    
    %load_ext ast_magic

To automatically load, add the following to your [IPython configuration file](https://ipython.org/ipython-doc/3/config/intro.html):
    
    c = get_config()
    c.InteractiveShellApp.extensions.append('ast_magic')
    
## Usage

Investigating operator precedence:

    In [39]: %ast print(True or False and True)
    Module(
        body=[
            Expr(
                value=Call(
                    func=Name(id='print', ctx=Load()),
                    args=[
                        BoolOp(
                            op=Or(),
                            values=[
                                Constant(value=True),
                                BoolOp(
                                    op=And(),
                                    values=[
                                        Constant(value=False),
                                        Constant(value=True)])])],
                    keywords=[]))],
        type_ignores=[])
    True
        
You can use it in a cell too:

    In [1]: %%ast
       ...:
       ...: def fibonacci(n: int) -> int:
       ...:     if n <= 1: return 1
       ...:     return fibonacci(n - 2) + fibonacci(n - 1)
       ...:
    Module(
        body=[
            FunctionDef(
                name='fibonacci',
                args=arguments(
                    posonlyargs=[],
                    args=[
                        arg(
                            arg='n',
                            annotation=Name(id='int', ctx=Load()))],
                    kwonlyargs=[],
                    kw_defaults=[],
                    defaults=[]),
                body=[
                    If(
                        test=Compare(
                            left=Name(id='n', ctx=Load()),
                            ops=[
                                LtE()],
                            comparators=[
                                Constant(value=1)]),
                        body=[
                            Return(
                                value=Constant(value=1))],
                        orelse=[]),
                    Return(
                        value=BinOp(
                            left=Call(
                                func=Name(id='fibonacci', ctx=Load()),
                                args=[
                                    BinOp(
                                        left=Name(id='n', ctx=Load()),
                                        op=Sub(),
                                        right=Constant(value=2))],
                                keywords=[]),
                            op=Add(),
                            right=Call(
                                func=Name(id='fibonacci', ctx=Load()),
                                args=[
                                    BinOp(
                                        left=Name(id='n', ctx=Load()),
                                        op=Sub(),
                                        right=Constant(value=1))],
                                keywords=[])))],
                decorator_list=[],
                returns=Name(id='int', ctx=Load()))],
        type_ignores=[])