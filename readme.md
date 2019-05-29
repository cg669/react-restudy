# 重新学习react---从每一个细节开始

------

因为react更新了很多细节，并且结合自己近几年使用，觉得有必要重新认识一下她：

> * 整理知识，学习笔记
> * 新功能，新特性

![cmd-markdown-logo](https://www.zybuluo.com/static/img/logo.png)

------

## context

Context 设计目的是为了共享那些对于一个组件树而言是“全局”的数据，例如当前认证的用户、主题或首选语言。

### 1. 栗子[^code]

```javascript
        const themes = {
            light: {
                color: '#000000',
                background: '#ffffff',
            },
            dark: {
                color: '#ffffff',
                background: '#000000',
            },
        };
        const ThemeContext = React.createContext({
            theme:themes.light,
            toggleTheme: ()=>{}
        });

        function ThemeToggleButton(){
            return <ThemeContext.Consumer>
                {
                    ({theme,toggleTheme}) => 
                    <button 
                        style={{backgroundColor: theme.background,color:theme.color}} 
                        onClick={toggleTheme}>
                        点我变色
                    </button>
                }
            </ThemeContext.Consumer>
        };

        function Content(){
            return <div>
                <ThemeToggleButton/>
            </div>
        };

        class Box extends React.Component{
            constructor(props){
                super(props)
                this.toggleTheme = () =>{
                    // console.log(this.state)
                    this.setState(state=>({
                        theme: state.theme === themes.light ? themes.dark : themes.light
                    }))
                }
                this.state = {
                    theme:themes.light,
                    toggleTheme: this.toggleTheme
                }
            }
            render(){
                // console.log(this.state)
                return <ThemeContext.Provider value={this.state}>
                    <Content/>
                </ThemeContext.Provider>
            }
        };

        ReactDOM.render(
            <Box/>,
            document.getElementById('demo')
        )
```

------

再一次感谢您花费时间阅读这份欢迎稿，点击 <i class="icon-file"></i> (Ctrl+Alt+N) 开始撰写新的文稿吧！祝您在这里记录、阅读、分享愉快！

作者 [@zcg][3]     
2019 年 05月 29日    


