<template>
    <div class="container">
        <h1>Filtrado GitHub</h1>
            
            Organización: <input type="search" v-model="searcher" placeholder="Lemoncode">

        <table className="table" v-if="searcher === ''">
            <thead>
                <tr>
                <th>Avatar</th>
                <th>Id</th>
                <th>Name</th>
                <th>Organization</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="member in members" :key="member.id">
                    <td><img v-bind:src="member.avatar_url" /></td>
                    <td>{{member.id}}</td>
                    <td>{{member.login}}</td>
                    <td>Lemoncode</td>
                </tr>
                <tr>
                    <td><img src="https://estaticos.muyinteresante.es/media/cache/1140x_thumb/uploads/images/gallery/59c4f5655bafe82c692a7052/gato-marron_0.jpg" /></td>
                    <td>123456</td>
                    <td>Luis</td>
                    <td>Microsoft</td>
                </tr>
                <tr>
                    <td><img src="data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkGBxAQEBAQEBAPEBAPEA8PDxAPDw8PDxAPFRUWFhUVFRUYHSggGBolGxUVITEhJSkrLi4uFx8zODMtNygtLisBCgoKDQ0NDw8PDisZFRkrKysrKysrKzc3KzctKystNy0tLTctLS03KzctNy03LSs3KystKystKysrKy0rLSsrK//AABEIAOEA4QMBIgACEQEDEQH/xAAcAAACAgMBAQAAAAAAAAAAAAAAAQIFAwQGBwj/xAA4EAACAQIFAgQEBAUDBQAAAAAAAQIDEQQFEiExQVEGYXGBEyIykQehscEjQlJy0RQz4WJzkvDx/8QAFwEBAQEBAAAAAAAAAAAAAAAAAAECA//EABkRAQEBAQEBAAAAAAAAAAAAAAABEQIxIf/aAAwDAQACEQMRAD8A9nbFcTAAAAAAAYCAYAAAMBASQwIASIgAhgACGIAA18VjqdL/AHJxj2Te79jNRmpRUou6fDAkAAAAAAAwAAAAAewAARFgNiCgAAAABgAAADR5x4/8Q1o4z/T0akqSo04SvF2vOW+/dWsekI8W/ExSp5rKUl8tWjSlB+l0/wBPzM9eLz66Dwz+JP8AEjh8wShqajDEx+i/TWunrwekJ33Tunw0fPOYYVVIO291dFh4P/ESvgf4FePxqMeE5fxIr/pb59CTpbHuwjnMq8dYHEJaZuLfSUWmWrzmh/Ua1luhcrnntCzeptLbZdTFW8SYeEXKTkkld/KNhi2RyfjLxhHCNYejapipq6j0pRf80vPsjkvFv4rVU/hYGko3TTq1d2vNJFD4Xwsqs5Yio/iVJu85ya1Tk+W7+iRL0sjpMKp1LzquUpvduTbd2dn4ErSlhGpNtwqzhv0tY5OU9G1lfy8jsPBlJxwkZNWdWdSrbbiT2/JIzz6114vRDEzowAQAA7gIYAAAAwAAExDYgAAABgAAAAAEonmn42YRKGFxFt4TlTl/bJX/AFR6XE4z8XqSlls9r2qU2vLfklWPL8LmUNFtWp2soSSa/wAo57OMBOpPVGDjblrhEcPaTjeEr3Vn09+qOxy/GU4xsouX926Xu9zm3VP4Wy+vBtvdXWz/AGOyhUkrubem3F+GVM83jBNJJPnbhFZmGcvTKXTmxB0azyOpRs7K9r/f9mSxuMjXptR2unt1ucJTxeqLld3a2/P/AIMyzd0mkuHZjFYqmU1XOTa+VvnrZdDoMojKlZOKirXXNzJgsbBrVJrffT1fYs4zpzjd3v0s+V5v1CK3Ms7tJJXu2o6rbK7te/ue2Zfh1TpU6cfphCMF6JWPnrM3VnVhDSo3ktMXdLv+x9AZNUk6FPX9eiOr1sb5TpuCY2Jm2CAAALgAAMQDAkAABEQ2IAAAAYCABgIlEInFFJ42pRng60JWtJbX7l6jkvHOIvFU+j5JVjx+tl6clpUdn0bt9rkq60xsu32LnEU4Q3+m3kkaM6q3fw5SSu7qL4Xmzm6OdUpJ2cvQ1sbVlZrp2N7NXP8Ahz0RiqskoLWtTvxddCWFp3nKnOnapHdxb5XdFTVZh6MnGLvtu+3Uz4/CWeveyUUvI6KhkjqQWjZJJ268syYjAx0SVRPRB3k+y4sgK/A1NKjfqrq/buXuArRe10u3HHkc5icx01KcIQjTjLQviVLSbhuo7dFsXFDDT1unKmtSSevW+Hw0hSVZ1cujWnHVqaTTUVLSrrh7HqHh2relGLvdJLc81wGGcGrS3Tt5r1PQvDtRuKTd7Dk6XzAAOjBAAAAAADAQATAQBCEDAKAAAgAAQDJxQoonwgrHXraU2ef+JManJyfsXPibNLfJHfzvwchmiUoXk+NzPVakVco/Fd3FNK/K/Q0qeNUG6baUeOrt/g3o4iFtMWr9uChziEotybbtx0fsYab9fL6VWNNVKc6nwnenKnKCvH+mSbv9jSq6/wDWUqk6ahG2hR6qCXLfU1MtzCa2je3bYsMfUb0yk7yinpj5vqPqSSOkyDeMrfz8egvEWGapfDgrOck2/R3Nnw3SSpQl3in6mfxLSlUpRdP6oTv5uLA5bE5VCsqUqmGm6lOyfwpRVOoul7u6RvqTg5Sqafi1LXUfpp04q0Yo18Rms6fyuyaRWUq+uWp3d3xfcWkkdVl83Jppv9jsshupW/Q43KsPspfMn7na5Gn67FnpXQjIjOjAAYggAACgAAIYAACAGAAIAABoRKIGSJzviTOHC8IvfuXuIqWizzjPcQ5Tk7X3ZLWoqqledSpvv1u7m9Uo64W7GngKe7fBuOk73W/d3ObSrhl8U7tK667lhh8vjU2krru3b8zZhTT6W9f3MkU1JcyfRJceb7ICnzPIIULOlDVe/wDNtf1KidGUlNypWcYylGz2clay4/8AbHoksPTxFPTJXtw/8HMZjk6pyUrXe8fpu2nzwXBw2AzrEWdOUnHQ1og/l23624Om8C5liq8pKsk6Kcvn5u78Lul3MGbYPXGEPhNODVpW309kXGUNQ+XUtNrKCX0+WwGPNMshUxLThK0rWkrtccW7mng/D/w6zvdxTum1Y7DA4O71/L6pb29eTYq0IuWzXnxZjDWnhIpWVlby3OqyyjbfuVOHwEW18tn3OjwtPTFI1IzayjGkDNMkAxAAAACAYgJAAAJiAYCAAACSZEUnsFV2c4rTFpdTz3NMTu9/2Ovzism2t9u62OGzOrFSd5fZK5jpqJ4S+2+3vctqVuF7nPUsQuFJ+nH3Zb4Go2uj9DKrKnSuzP8AASTvx1v19upHDp9vVs2FFvnjourA0IVaqk5xXyKySezb7/bobscdGW0lpfZ8fczKPfp06GOVDuiolNQns1F/YhChSjuox9drkHh12I/BsBs1MRtaCV+lzXo4aSeqbu31WyfqjJTp2NynurFG3l7t/guqZR0Ni4oS2NRGwkJgmDKhMQ2IIAAAAQxASABAJgDAAAQFAQqPYmYK0iKoM6it2ee5zKLk3u7c2PQM6leLOBzSja9rdzHTUaeEqQbWz7K7R0mA2souPsjkYJp3srL7/foX+W1nLTaNori9933MtOqp9LmzCb6+xp4eXfdv8jI6jvZc/exWW23bd9tkZLdzW172urrnq/UzaihyW4rEb7k7ASUU0OnTCiuhmaCCnyW2F4Kii3ct8NwaiNmI2KIyhCGAQgGIAAAAYAAEWIGAAAgKBs0sVM2psqsfVsSqqMync5LPKfy7bHRYypcrMZBOLvxYxWo5CnXV7NbR6vi5v4XG2aSTcnu5OXCK3MoaJ2ik3ffskGHna/yqTe7V7K3mzKu2yzFxlF/M3bq+fYtaCul06+ZwuEzSScVxG6V0rbc7LsXWX5nd7PvdN/YDqYUUuOTKm7Gvh690r823NqE0yoxxRkgyU0ka7qpNeYG3B2Jt33TNGrVtwa9LGPj9Si2pR3Legtirwbvuy2pcGoyzRGJDKAAEAxMACAAABgAAY2AMQDEAmyiNR7FLmRcVGU2Z8EqxzeNlvvwYZVLqysLNKq469EVMpSWyk/MxWowZvTTT4uupzlKDlKzi1G97XtfzZfY2o7bK76ruVGIqK15Jqz+ZPo/PuZVZUcI5Kyta93L06X7EqtCVP5k+DVwGNTWytFJPfr5suIyU4pS35YVs5DnF3ok+bu79jqKc9vVnneIw/wAKUJxe2pKS82dlga7cE32TZUq0q1tku5WY7GKMkr7/ALkcVidPzdkzh81zWTam3dObkunPCCO5p5jBuykrrpcyxndnn+VVJylqf/J2OX1HLZ3t5hXY5ZO6RcUuCjyqJe0zcYZEMSAoYCAIAACgGIEQTAAAxMQ2JgJiYSIsCNRlFm8ti8mUueQ+RtdBVjkMd1fsV9uhY4jzK6tdXtyc621cYlvyiirTSk4vdX45LvFQlp482c7mVGUXqSIFjcXKGlx6u8bq7feRHCZpJz3blb9Sxy+hTqq8ldtfM3+i7G/h8khe/T06eQVgoY6M/llxJW36P/J1mGqr4d78JIoKuR3+m2z26GX4sqdKqpbaUmrhEvEGZKFKW61NWir8s5ChhJ1LOfEbO3QyVq7rTbe6sv1Nl15fSuOvl5eoFxl9NJK3kdXldM5TK5NpbfY6vLNkrb+RYV0+WF1Ap8BZJFvTexuMVlQyKJFAAgCGAgAYIAAkAABjZFkmRAiyLZJkGAmaGPpKSdzfZr1kFed5xLTNpcIr41U+ef2On8SZe3FyirtbnH0MNPXumlbf0MWNRZzinC/t6lHmdC6Zt5lmFmoJ7JcGtOvGSvexFV+SyUW493dLz/8Alzo6dRbOTa7JHO0ko1F7/mXuFts+vTr9iC2pSXT8zFj8KqtOcX/Mug4WMylt5gedqDpylG1rPqRoyT+rfsvPuyz8SW+M7Lp9yrgmpceYHSZbUV0k9K29GdVl1VRlG/F7nH5dOyV9/a5cqTcdmwPQKeKfEt0/uvQtcNPbv59zn6CbjDzSLjDStGPojpGFimMxwkTuUMBXAIYCGADQhgSAQAQZEbIsCMiLJMTAgzHNGQTQVXYrD6jls/wsaUJVONjt3FHG/iDTbo9kml6kqx5njU5ybjLfqUuLzeVNuPLV+TqcJg/4bqytFeexzmMyarjq+nCU3U0r55xXyJ+cuL+RiK18DnTk/mR2OUYtTjfqleyKPC+AsZB70pJ+1i3wWRYrDRnKrDTFqMU783e5cNdDhaq73JfF3sVuHxNkZnW6tq37+RlVFnqcsRFcbXNXGUdMU+t+CyzCg5VITSule/R29PsUWeYprurP7MCywNTZf0re/X0OgymnOvUUVdLa/ktnc4zLMUpNRa+q26PXfC2XKNNz2u4xivYuJVhh+VFXsrJexbQ6eRq0KNjJNu8X5pP0exqMrOjK5lZq4fk2mUCYyKGVDQxDAYAgAkAgCoMiybRFoIiyJNohJARYmSaIsCJr4vAUqytUjqXa9kbNgCqOfhDANpuhqUeISqVJU/8Awbs/csYYOEEowjGEVxGMVFL2RtMQGs8Oik8UYPVQa4SabfZX3OjbMGKpKcXFpNPm4HiOeVJ0pqnFP53BRlbZqXYt8strb5aloi3uk1a9jqPF/h+VZUHTjFyo1FOz2+Vfsc5gsPOGuKp1daTn9Em5Sct3HuYsalRlQ1Tg27Nqbfs1+tzkPEeBk5TjFOUl89rbqD4OyhKcZ/7dbRJSSl8OT0zWyRmyLJZ1ak51IPnmpD6qd7peqdySLXnXh7DVdavGWz7M+hMowuijDzhFv3Rr5fk1OH8kd/JF7Shskum3saxjVdqknYnCDa3RvyoLsNU+xYiUI2JOQKItJVNMkRiiVghokiKRJIBgA7AFgJWAKj1ISAAIEQABEQABCAAB8i6gAEO4nw/RjADVxHT+1/oV+G/3KXv+gAQZcT9Ef+5+5lo8y9WAAb9I26IAUZ5iYABjZEAIGiQAUBIAAY4gAEwAAj//2Q==" /></td>
                    <td>123457</td>
                    <td>Juan</td>
                    <td>Microsoft</td>
                </tr>
                <tr>
                    <td><img src="https://is2-ssl.mzstatic.com/image/thumb/Purple1/v4/0c/dd/e0/0cdde0ef-3151-2adb-afbc-bc0ffaace9ce/source/256x256bb.jpg" /></td>
                    <td>123458</td>
                    <td>María</td>
                    <td>Microsoft</td>
                </tr>
            </tbody>
        </table>

        <table className="table" v-if="'Lemoncode'.toUpperCase().startsWith(searcher.toUpperCase()) && searcher !== ''">
            <thead>
                <tr>
                    <th>Avatar</th>
                    <th>Id</th>
                    <th>Name</th>
                    <th>Organization</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="member in members" :key="member.id">
                    <td><img v-bind:src="member.avatar_url" /></td>
                    <td>{{member.id}}</td>
                    <td>{{member.login}}</td>
                    <td>Lemoncode</td>
                </tr>
            </tbody>
        </table>

        <table className="table" v-if="'Microsoft'.toUpperCase().startsWith(searcher.toUpperCase()) && searcher !== ''">
            <thead>
                <tr>
                    <th>Avatar</th>
                    <th>Id</th>
                    <th>Name</th>
                    <th>Organization</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td><img src="https://estaticos.muyinteresante.es/media/cache/1140x_thumb/uploads/images/gallery/59c4f5655bafe82c692a7052/gato-marron_0.jpg" /></td>
                    <td>123456</td>
                    <td>Luis</td>
                    <td>Microsoft</td>
                </tr>
                <tr>
                    <td><img src="data:image/jpeg;base64,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" /></td>
                    <td>123457</td>
                    <td>Juan</td>
                    <td>Microsoft</td>
                </tr>
                <tr>
                    <td><img src="https://is2-ssl.mzstatic.com/image/thumb/Purple1/v4/0c/dd/e0/0cdde0ef-3151-2adb-afbc-bc0ffaace9ce/source/256x256bb.jpg" /></td>
                    <td>123458</td>
                    <td>María</td>
                    <td>Microsoft</td>
                </tr>
            </tbody>
        </table>
    </div>    
</template>

<script>
    import { defineComponent } from 'vue';
    import API from '../api'

    export default defineComponent ({
        data() {
            return {  
                searcher: 'Lemoncode',
                fields: ['avatar_url', 'id', 'login'],
                avatar_url: "",
                id: "",
                login: "",
                members: [],
            }
        },
        mounted() {
            API.get('https://api.github.com/orgs/lemoncode/members')
                .then(response => {
                    this.members = response.data;
            });
        },
        watch: {
            searcher(currentValue) {
                this.$emit('input', currentValue)
            }
        },
    });
</script>

<style scoped>
    img {
        width: 5rem;
    }
</style>