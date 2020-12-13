# lyne-comment-solution

Now just write Chinese user guide.

Personal documentation comments and normal comments standard, WIP.
En, solution is personal standard.



个人所用文档注释和普通注释规范, WIP.

## Project Background

### 需要描述规范化

或许时候, 代码注释想要表达的意思都是模式化的, 但是由于开发者的母语或是个人注释的习惯, 导致描述得千变万化.
即使是一个写的注释, 描述同一个意思的方法也不尽相同.

### 独立于程序语言的文档注释

## Draft

[lyne-comment-solution.xml](./lyne-comment-solution.xml)

## 示例 

### 示例1: `TypeScript` code 

下面的 `TypeScript` code 演示 lyne408 这种注释风格.

```typescript
/**
 * <functionalParameterType function="filterFilesAndDirectories" />
 */
export type FilterFilesAndDirectoriesParameter = {

	/**
	 * 被筛选的目录, 可为 绝对路径 或 相对路径
	 *
	 * <necessity required />
	 */
	dir: string

	/**
	 * 是否获取文件
	 *
	 * 为 false 表示不获得任何文件, 显然也不会进行筛选
	 *
	 * <necessity optional />
	 */
	isGetFiles?: boolean

	/**
	 * 是否获取文件夹
	 *
	 * <necessity optional />
	 */
	isGetDirectories?: boolean

	/**
	 * 文件名/文件夹名 含有 inclusions 中任意一个则认为符合筛选条件
	 *
	 * <necessity optional />
	 *
	 * <propertyDependencies mode="anyOf">
	 *  <property name="isGetFiles" value="true" />
	 *  <property name="isGetDirectories" value="true" />
	 * </propertyDependencies>
	 */
	inclusions?: Array<string>

	/**
	 * 筛选文件扩展名的数组
	 *
	 * 如果 ${inclusions} 和 ${extnames} 都为非空数组, 则形成类似矩阵的条件.
	 *
	 * <necessity optional />
	 *
	 * <propertyDependency name="isGetFiles" value="true" />
	 */
	extnames?: Array<string>

	/**
	 * whether to get absolute path
	 *
	 * <necessity optional />
	 *
	 * <if value="true">
	 * 	these returned files or directories or both is the absolute path not these names
	 * </if>
	 *
	 * <propertyDependencies mode="anyOf">
	 *  <condition value="true" />
	 *  <property name="isGetFiles" value="true" />
	 *  <property name="isGetDirectories" value="true" />
	 * </propertyDependencies>
	 *
	 * <design>
	 * 	absolute path is better for CLI program arguments
	 * </design>
	 */
	isGetAbsolutePath?: boolean
}
```

#### 说明

`<functionalParameterType />` 表示转为某个函数编写的参数类型.

`<necessity required />` 表示必须.

`<necessity optional />` 表示可选.



```xml
<propertyDependencies mode="anyOf">
	<property name="isGetFiles" value="true" />
	<property name="isGetDirectories" value="true" />
</propertyDependencies>
```

`<propertyDependencies mode="anyOf">` 表示当前属性依赖于另外的属性.

 `mode="anyOf"` 表示依赖其中任意一个.

子元素 `<property>` 表示依赖的单个属性.



```xml
<if value="true">
	these returned files or directories or both is the absolute path not these names
</if>
```

`<if value="true"> description </if>` 表示值为 `true` 的描述.



```xml
<design>
	absolute path is better for CLI program arguments
</design>
```

`<design> description </design>` 表示为什么要这样设计. 



