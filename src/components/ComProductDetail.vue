<template>
   <main>  
        <div class="menu">
            <h2 class="menu-title">TRÀ</h2>
            <div class="menu-carousel">
                <div class="menu-item">
                    <img :src="product.image" alt="TRÀ">
                    <div class="menu-item-info">
                        <h3>{{product.name}}</h3>
                        <p>{{product.description}}</p>
                        <p>{{product.price}}</p>
                    </div>
                </div>
                <div v-if="product.quality==0">
                    <p>Hết Hàng</p>
                </div>
                <div v-else>
                    <button @click="addToCard(product)">Mua Hàng</button>
                </div>
            </div>
        </div>  
    </main>
</template>

<script>
import items from '@/data/items'
import cart from '@/data/cart'
export default {
    //nhận về id
    data()
    {
        return{
            //Tạo ra đối tượng
            product:{},
            cart:cart
        }
    },
    //dữ liệu luôn được load về trước component
    mounted(){
        let id = this.$route.params.id
        //dò trong dữ liệu
        this.product=items.find(x=>x.id ==id)
    },
    methods:{
        addToCard(product)
        {
            //kiem tra san pham co trong gio hang hay chua
            const infoproduct = this.cart.find(x=>x.id==product.id)
            if(infoproduct)
            {
                //if(infoproduct.quantity<=product.quality)
                if(product.quality>0)
                {
                    infoproduct.quantity+=1;
                }
                
            }
            else
            {
                if(product.quality > 0){
                    const newproduct = {...product,quantity:1}
                    this.cart.push(newproduct)
                }
                
            }
            product.quality--
        }
    }
}
</script>

<style>
.menu {
    text-align: center;
    padding: 40px 20px;
    background-color: #fff;
}

.menu-title {
    font-size: 32px;
    margin-bottom: 20px;
}

.menu-carousel {
    display: flex;
    justify-content: center;
    align-items: center;
    overflow: hidden;
    position: relative;
    max-width: 100%;
    animation: slideIn 1s ease-in-out;
}

.menu-item {
    position: relative;
    flex: 0 0 25%;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    border-radius: 8px;
    margin: 0 10px;
    overflow: hidden;
    transition: transform 0.3s ease;
}

.menu-item img {
    width: 100%;
    transition: transform 0.3s ease;
}

.menu-item-info {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.7);
    color: #fff;
    text-align: left;
    padding: 20px;
    opacity: 0;
    transition: opacity 0.3s ease;
}

.menu-item:hover .menu-item-info {
    opacity: 1;
}

.menu-item:hover img {
    transform: scale(1.1);
}

.menu-item-info h3 {
    font-size: 18px;
    margin: 0 0 10px;
}

.menu-item-info p {
    margin: 0;
    color: #ccc;
}

.menu-navigation {
    position: absolute;
    top: 50%;
    width: 100%;
    display: flex;
    justify-content: space-between;
    transform: translateY(-50%);
}

.menu-navigation i {
    background-color: rgba(0, 0, 0, 0.5);
    color: #fff;
    padding: 10px;
    border-radius: 50%;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

.menu-navigation i:hover {
    background-color: #fcb034;
}
</style>