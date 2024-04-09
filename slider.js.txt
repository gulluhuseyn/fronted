const slide = document.createElement("div");
slide.classList.add("slide");
const rightBtn = document.getElementById("right"); 
const leftBtn = document.getElementById("left");
let Index = 0;
let images = [];

function viewslide(index) {
    slide.innerHTML = "";
    const img = document.createElement("img");
    img.src = images[index];
    slide.appendChild(img);
}

function nextphoto() {
    Index = (Index + 1) % images.length;
    viewslide(Index);
}

function prevphoto() {
    Index = (Index - 1 + images.length) % images.length;
    viewslide(Index);
}

rightBtn.addEventListener("click", nextphoto);
leftBtn.addEventListener("click", prevphoto);

fetch('https://fakestoreapi.com/products')
    .then(res => res.json())
    .then(apiimages => {
        images = apiimages.map(a => a.image);
        viewslide(Index);
    });

document.body.appendChild(slide);
