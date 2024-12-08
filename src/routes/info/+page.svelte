<script>
    import Navbar from '../../components/NavBar.svelte';
    import LoginModal from '../../components/LoginModal.svelte';
	import Category from '../../components/Category.svelte';

    let showLoginModal = false;
    let isAuthenticated = false;
    const nullUser = {"username":null, "profilePic":null};
    let user = nullUser;

    const items = {"image": 'thumbnails/kimetsunoyaiba.png',"title": "Thanh Gươm Diệt Quỷ" ,"category":["Shounen", "Tragedy", "Drama", "Historical"], "author": "Gotouge Koyoharu", "status": "Đã hoàn thành", "fav":20000000,"view":10000000 ,"fol":100000, "desc":"Kismetu no Yaiba – Tanjirou là con cả của gia đình vừa mất cha. Một ngày nọ, Tanjirou đến thăm thị trấn khác để bán than, khi đêm về cậu ở nghỉ tại nhà người khác thay vì về nhà vì lời đồn thổi về ác quỷ luôn rình mò gần núi vào buổi tối. Khi cậu về nhà vào ngày hôm sau, bị kịch đang đợi chờ cậu…"}

    function toggleLoginModal() {
    showLoginModal = !showLoginModal;
  }
    /**
	 * @param {any} loggedinUser
	 */
    function handleLoginSuccess(loggedinUser) {
        isAuthenticated = true;
        user = loggedinUser;
        showLoginModal = false;
    }

    function logout() {
        isAuthenticated = false;
        user = nullUser;
    }
</script>
<Navbar
  isAuthenticated={isAuthenticated}
  user={user}
  onLogin={toggleLoginModal}
  onLogout={logout}
/>

<div class="w-[1307px] h-[1643px] relative bg-white rounded-[10px] shadow mt-32">
    <div class="pl-11 pr-7 py-[23px] left-[1px] top-0 absolute justify-end items-center gap-[38px] inline-flex">
        <img class="w-[275px] h-[321px] relative rounded-[10px] shadow" src={items.image} alt={items.title}/>
        <div class="size-fit relative bg-[#d9e4f8] rounded-[10px] flex-col justify-start items-start flex p-16">
            <div class="w-[350px] h-[57px] text-black text-2xl font-semibold font-['Inter']">{items.title}</div>
            <div class="w-[367px] h-40 flex-col justify-center items-start inline-flex">
                <div class="self-stretch grow shrink basis-0 justify-center items-start gap-[35px] inline-flex">
                    <div class="w-[120px] h-8"><span style="text-black text-xl font-medium font-['Inter']">Tác giả</span><span style="text-black text-xl font-normal font-['Inter']">: </span></div>
                    <div class="w-[212px] h-8 text-black text-xl font-normal font-['Inter']">{items.author}</div>
                </div>
                <div class="self-stretch grow shrink basis-0 justify-center items-center gap-[35px] inline-flex">
                    <div class="w-[120px] h-8"><span style="text-black text-xl font-medium font-['Inter']">Tình trạng</span><span style="text-black text-xl font-normal font-['Inter']">: </span></div>
                    <div class="w-[212px] h-7 text-black text-xl font-normal font-['Inter']">{items.status}</div>
                </div>
                <div class="self-stretch grow shrink basis-0 justify-center items-center gap-[35px] inline-flex">
                    <div class="w-[120px] h-8"><span style="text-black text-xl font-medium font-['Inter']">Lượt thích</span><span style="text-black text-xl font-normal font-['Inter']">: </span></div>
                    <div class="w-[212px] h-7 text-black text-xl font-normal font-['Inter']">{items.fav}</div>
                </div>
                <div class="self-stretch grow shrink basis-0 justify-center items-center gap-[35px] inline-flex">
                    <div class="w-[120px] h-8"><span style="text-black text-xl font-medium font-['Inter']">Lượt xem</span><span style="text-black text-xl font-normal font-['Inter']">: </span></div>
                    <div class="w-[212px] h-7 text-black text-xl font-normal font-['Inter']">{items.view}</div>
                </div>
                <div class="self-stretch grow shrink basis-0 justify-center items-center gap-[5px] inline-flex">
                    <div class="w-[150px] h-8"><span style="text-black text-xl font-medium font-['Inter']">Lượt theo dõi</span><span style="text-black text-xl font-normal font-['Inter']">: </span></div>
                    <div class="w-[212px] h-7 text-black text-xl font-normal font-['Inter']">{items.fol}.000</div>
                </div>
            </div>
            <section class="h-[51px] pl-3.5 pr-[477px] py-2.5 justify-start items-start gap-[9px] inline-flex">
                <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-4 gap-4">
                    {#each items.category as category}
                    <Category {category} />
                    {/each}
                </div>
            </section>
            <div class="w-[132px] px-[11px] pt-2 pb-[5px] bg-[#1976f0] rounded-[10px] shadow justify-center items-center inline-flex">
                <button class="w-[110px] h-[33px] text-center text-black text-base font-medium font-['Inter']">Bắt Đầu Đọc</button>
            </div>
            <div class="w-[132px] px-[11px] pt-2 pb-[5px] bg-[#fa7d7d] rounded-[10px] shadow justify-center items-center inline-flex">
                <button class="w-[110px] h-[33px] text-center text-black text-base font-medium font-['Inter']">Thích</button>
            </div>
            <div class="w-[132px] px-[11px] pt-2 pb-[5px] bg-[#57f9a5] rounded-[10px] shadow justify-center items-center inline-flex">
                <button class="w-[110px] h-[33px] text-center text-black text-base font-medium font-['Inter']">Theo dõi</button>
            </div>
        </div>
    </div>
    <div class="pl-[45px] pr-[49px] pt-[26px] left-[-1px] top-[400px] absolute flex-col justify-end items-start gap-1.5 inline-flex">
        <div class="w-[244px] h-9 text-[#363994] text-xl font-bold font-['Inter']">Thông Tin Sách</div>
        <div class="w-[1214px] h-[126px] text-black text-xl font-medium font-['Inter']"><br/>{items.desc}</div>
        
    </div>
</div>
{#if showLoginModal}
<LoginModal 
    on:loginSuccess={(e) => handleLoginSuccess(e.detail)} 
    on:close={()=>{showLoginModal=false}}/>

{/if}