>     
>     它那用來被丟回當後備方案用的退路兜底基本預設值 (The fallback values) 說到底其實就跟 Cube、Sphere、Cone，還有 Cylinder 那些老兄們如出一轍。他們這輩子最大的命運：大概也就是都給一起縮進然後塞進同一個用來包覆他們的容積界線 (volume/bounds) 框體宿命裡的那些爛帳這點不會變。"""
>     customData = {
>         dictionary extraPlugInfo = {
>             bool implementsComputeExtent = true
>         }
>     }
> ) {
>     double size = 2.0 (
>         doc = """這一道屬性 (Indicates the length) 指著這該死方塊身上每個冰冷邊緣的實際邊緣長度。 如果您老兄今天有種去敢撰寫了
>         \\em size 您就非得被強逼無可避免地也要去給它把這條 \\em extent 也一併給撰寫上去。
>         
>         \\sa GetExtentAttr()"""
>     )
> 
>     float3[] extent = [(-1.0, -1.0, -1.0), (1.0, 1.0, 1.0)] (
>         doc = """這條名為 Extent 強制拓展範圍線底限長度的破屬性 之所以破天荒會需要單獨為了 Cube 而被生生拿來重新界定一遍 (re-defined on Cube only) 不為甚麼，無非就是想被搞出個能夠作為預留備案、後路好走的後備退群防線基本數值來用（provide a fallback value）。
>         \\sa UsdGeomGprim::GetExtentAttr()."""
>     )
> 
> }
> ```

打造出這種五花八門全新的 prims 系列特製款家族型別，它可以既親民到有如在切上一塊像上面那個無聊爛透頂端代碼的生肉方塊那麼可笑簡單；或者當然了，如果您熱愛刺激的話，這事兒也可以被瘋狂複雜擴張上綱到猶如在無垠荒漠中獨自苦寫開天闢地構築「一套完完整整巨型神經網路錯綜複雜 `Mesh (多變網型體)`」般的驚心動魄！

---

> **📝 延伸閱讀**
>
> ↪ [USD Glossary - IsA Schema](https://graphics.pixar.com/usd/release/glossary.html#isa-schema)
