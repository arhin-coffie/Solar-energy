<template>
    <section class="services-view">
      <h2 class="section-title">Our Professional Services</h2>
      
      <div v-for="(service, index) in services" :key="index" class="service-section">
        <h3 class="service-header">{{ service.title }}</h3>
        <div class="service-carousel">
          <button class="nav-btn prev" @click="prevSlide(index)" aria-label="Previous">&lt;</button>
          
          <div class="carousel-track" :style="{ transform: `translateX(-${currentSlides[index] * 33.333}%)` }">
            <div 
              v-for="(image, imgIndex) in service.images" 
              :key="imgIndex" 
              class="service-image-container"
              @click="openModal(index, imgIndex)"
            >
              <img :src="image" :alt="service.title" class="service-image">
              <div class="image-overlay">
                <span class="view-text">View Details</span>
              </div>
            </div>
          </div>
  
          <button class="nav-btn next" @click="nextSlide(index)" aria-label="Next">&gt;</button>
        </div>
      </div>
  
      <!-- Service Modal -->
      <div v-if="selectedService !== null" class="service-modal" @click.self="closeModal">
        <div class="modal-content">
          <button class="close-btn" @click="closeModal" aria-label="Close Modal">&times;</button>
          <div class="modal-carousel">
            <img 
              :src="services[selectedService].images[selectedImageIndex]" 
              :alt="services[selectedService].title" 
              class="modal-main-image"
            >
            <div class="modal-thumbnails">
              <img
                v-for="(image, idx) in services[selectedService].images"
                :key="idx"
                :src="image"
                :class="{ active: idx === selectedImageIndex }"
                @click="selectedImageIndex = idx"
                :alt="`Thumbnail ${idx + 1}`"
              >
            </div>
          </div>
          <div class="modal-details">
            <h3>{{ services[selectedService].title }}</h3>
            <p>{{ services[selectedService].description }}</p>
          </div>
        </div>
      </div>
    </section>

    <section>
<NewRoom/>
    </section>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import NewRoom from './NewRoom.vue';
  
  const services = ref([
  {
    title: 'Solar Installation',
    description: 'Professional solar panel installation and maintenance services',
    images: [
      'https://images.pexels.com/photos/14613939/pexels-photo-14613939.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1', // Solar team installation
      'https://images.pexels.com/photos/30285845/pexels-photo-30285845/free-photo-of-technician-installing-solar-panels-on-rooftop.jpeg?auto=compress&cs=tinysrgb&w=600', // Rooftop solar array
      'https://images.pexels.com/photos/9800008/pexels-photo-9800008.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1', // Technician installing
      'https://images.unsplash.com/photo-1613665813446-82a78c468a1d', 
      'https://images.pexels.com/photos/13932269/pexels-photo-13932269.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1', // Solar farm
      'https://images.pexels.com/photos/8853513/pexels-photo-8853513.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1' // Residential installation
    ]
  },
  {
    title: 'CCTV Installation',
    description: 'Professional security system installation and configuration',
    images: [
      'https://images.pexels.com/photos/96612/pexels-photo-96612.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1', // Camera installation
      'https://images.pexels.com/photos/7364948/pexels-photo-7364948.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1', // Security room
      'https://images.pexels.com/photos/29280895/pexels-photo-29280895/free-photo-of-close-up-of-a-modern-security-camera-in-action.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1', // Camera on wall
      'https://images.pexels.com/photos/31036015/pexels-photo-31036015/free-photo-of-monochrome-surveillance-camera-on-urban-streetlight.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1', // Multiple cameras
      'https://images.pexels.com/photos/207574/pexels-photo-207574.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1', // Camera closeup
      'https://images.pexels.com/photos/5589597/pexels-photo-5589597.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1' // Monitoring station
    ]
  },
  {
    title: 'Electrical Wiring',
    description: 'Professional electrical wiring services for all building types',
    images: [
      'https://images.pexels.com/photos/257736/pexels-photo-257736.jpeg', // Electrician at work
      'https://images.pexels.com/photos/17018102/pexels-photo-17018102/free-photo-of-electricians-working-with-power-lines.jpeg', // Commercial wiring
      'https://images.pexels.com/photos/26100225/pexels-photo-26100225/free-photo-of-man-fixing-in-electric-box.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1', // Wiring organization
      'https://www.mspurelife.com/cdn/shop/articles/Air_Purifier_vs_Air_Conditioner-_Can_They_Work_Together.jpg?v=1720158350&width=1000', // Industrial wiring
      'https://images.pexels.com/photos/7286015/pexels-photo-7286015.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1', // Safety testing
      'https://images.pexels.com/photos/10871585/pexels-photo-10871585.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1' // Residential wiring
    ]
  },
  {
    title: 'Air-conditioning',
    description: 'AC system installation and maintenance services',
    images: [
      'https://www.paradigmcooling.co.za/articles/wp-content/uploads/2024/05/AC-service-technician-doing-repair-jpg.webp', // AC installation
      'https://aws-obg-image-lb-4.tcl.com/content/dam/brandsite/global/images-for-blog/ac-maintenance-for-lasting-system-pc.jpg?t=1731490541012&w=2560', // Technician servicing
      'https://aws-obg-image-lb-4.tcl.com/content/dam/brandsite/global/images-for-blog/ac-maintenance-for-lasting-system-image.jpg?t=1731490541016&w=1200&webp=true&dpr=1&rendition=2400', // Modern AC unit
      'https://aws-obg-image-lb-1.tcl.com/content/dam/brandsite/product/ac/light-commercial/ceiling-floor/toolkits/plp-banner-pc.jpg?t=1719817044667&w=2560&webp=true&dpr=1&rendition=2400', // Duct work
      'https://shop.haierindia.com/blog/wp-content/uploads/2024/07/alling-4-9-1024x576.jpg', // Maintenance
      'https://shop.haierindia.com/blog/wp-content/uploads/2024/07/alling-1-9-1024x576.jpg' // Thermostat install
    ]
  },
  {
    title: 'Fire Alarm Systems',
    description: 'Fire safety system installation and maintenance',
    images: [
      'https://images.pexels.com/photos/20614571/pexels-photo-20614571/free-photo-of-fire-alarm-button-on-a-gray-wall.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1', // Smoke detector
      'https://5.imimg.com/data5/SELLER/Default/2024/7/437309219/CN/DM/PJ/81270448/fire-alarm-system.png', // Fire sprinkler
      'https://images.pexels.com/photos/13060860/pexels-photo-13060860.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1', // Control panel
      'https://nwoss.com/wp-content/uploads/2021/05/Blog_FireAlarmSystems_EverythingYouNeedtoKnow-e1655918801379.png', // Emergency lights
      'https://www.epssecurity.com/wp-content/uploads/2019/08/ONXYwDet_USA_new_jpg.jpg', // Fire drill
      'https://www.epssecurity.com/wp-content/uploads/2019/08/IMG_20181213_100130-e1565626544268.jpg' // Installation team
    ]
  },
  {
    title: 'Generator Servicing',
    description: 'Professional generator maintenance and repair',
    images: [
      'https://www.electricgeneratorsdirect.com/products-image/1000/030738_151596_1200_33353132592092f50ccae55df87f5e1e.jpg', // Large generator
      'https://s.alicdn.com/@sc04/kf/H2b373ec8742d43d8a36df84d07eb4a95c.jpg?avif=close', // Technician working
      'https://img.etimg.com/thumb/msid-69098659,width-300,height-225,imgsize-1235455,resizemode-75/.jpg', // Portable generator
      'https://images.unsplash.com/photo-1588854114873-8d7e0e05fecc', // Industrial generator
      'https://images.unsplash.com/photo-1588880331179-bc9b93a8cb5e', // Maintenance tools
      'https://images.unsplash.com/photo-1588853767490-c0f0c5d170f7' // Testing equipment
    ]
  }
]);
  const currentSlides = ref(services.value.map(() => 0));
  const selectedService = ref(null);
  const selectedImageIndex = ref(0);
  
  const nextSlide = (serviceIndex) => {
    if (currentSlides.value[serviceIndex] < 1) { // 6 images = 2 slides (0-1)
      currentSlides.value[serviceIndex]++;
    }
  };
  
  const prevSlide = (serviceIndex) => {
    if (currentSlides.value[serviceIndex] > 0) {
      currentSlides.value[serviceIndex]--;
    }
  };
  
  const openModal = (serviceIndex, imageIndex) => {
    selectedService.value = serviceIndex;
    selectedImageIndex.value = imageIndex;
  };
  
  const closeModal = () => {
    selectedService.value = null;
  };
  </script>
  
  <style scoped>
  .services-view {
    padding: 4rem 2rem;
    background: #f8fafc;
  }
  
  .section-title {
    text-align: center;
    font-size: 2.5rem;
    margin-bottom: 3rem;
    color: #1e293b;
    position: relative;
    padding-bottom: 1rem;
  }
  
  .section-title::after {
    content: '';
    position: absolute;
    bottom: 0;
    left: 50%;
    transform: translateX(-50%);
    width: 100px;
    height: 4px;
    background: #f59e0b;
    border-radius: 2px;
  }
  
  .service-section {
    margin-bottom: 5rem;
    margin: 4% 10%;
    padding: 4rem 0;
    background: white;
    border-radius: 1rem;
    box-shadow: 0 6px 6px -1px rgba(0, 0, 0, 0.1);
  }
  
  .service-header {
    font-size: 2rem;
    color: #0f172a;
    margin-bottom: 2rem;
    padding-left: 2rem;
    position: relative;
  }
  
  .service-header::before {
    content: '';
    position: absolute;
    left: 0;
    top: 50%;
    transform: translateY(-50%);
    width: 8px;
    height: 60%;
    background: #f59e0b;
    border-radius: 4px;
  }
  
  .service-carousel {
    position: relative;
    margin: 0 2rem;
    overflow: hidden;
    border-radius: 1rem;
  }
  
  .carousel-track {
    display: flex;
    transition: transform 0.5s cubic-bezier(0.4, 0, 0.2, 1);
    gap: 1rem;
    padding: 1rem;
  }
  
  .service-image-container {
    flex: 0 0 calc(33.333% - 1rem);
    position: relative;
    border-radius: 0.5rem;
    overflow: hidden;
    cursor: pointer;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }
  
  .service-image-container:hover {
    transform: translateY(-4px);
    box-shadow: 0 8px 15px rgba(0, 0, 0, 0.2);
  }
  
  .service-image {
    width: 100%;
    height: 400px;
    object-fit: cover;
    transition: transform 0.5s ease;
  }
  
  .image-overlay {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.4);
    display: flex;
    align-items: center;
    justify-content: center;
    opacity: 0;
    transition: opacity 0.3s ease;
  }
  
  .service-image-container:hover .image-overlay {
    opacity: 1;
  }
  
  .view-text {
    color: white;
    font-size: 1.25rem;
    font-weight: 500;
    text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
    transform: translateY(20px);
    transition: transform 0.3s ease;
  }
  
  .service-image-container:hover .view-text {
    transform: translateY(0);
  }
  
  .nav-btn {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background: rgba(255, 255, 255, 0.9);
    border: 1px solid #64748b;
    width: 80px;
    height: 80px;
    border-radius: 50%;
    cursor: pointer;
    box-shadow: 6 8px 8px rgba(19, 18, 18, 0.1);
    transition: all 0.3s ease;
    z-index: 100;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .nav-btn:hover {
    background: white;
    transform: translateY(-50%) scale(1.1);
    box-shadow: 0 6px 8px rgba(0, 0, 0, 0.15);
  }
  
  .prev {
    left: 1rem;
  }
  
  .next {
    right: 1rem;
  }
  
  .service-modal {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.9);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1000;
    backdrop-filter: blur(5px);
  }
  
  .modal-content {
    background: white;
    max-width: 1200px;
    width: 90%;
    border-radius: 1rem;
    overflow: hidden;
    position: relative;
  }
  
  .modal-main-image {
    width: 100%;
    height: 500px;
    object-fit: cover;
    border-bottom: 3px solid #f59e0b;
  }
  
  .modal-thumbnails {
    display: flex;
    gap: 1rem;
    padding: 1rem;
    overflow-x: auto;
    background: #f8fafc;
  }
  
  .modal-thumbnails img {
    width: 100px;
    height: 75px;
    object-fit: cover;
    border-radius: 0.5rem;
    cursor: pointer;
    opacity: 0.7;
    transition: all 0.3s ease;
    border: 2px solid transparent;
  }
  
  .modal-thumbnails img:hover {
    opacity: 1;
    transform: scale(1.05);
  }
  
  .modal-thumbnails img.active {
    opacity: 1;
    border-color: #f59e0b;
    transform: scale(1.08);
  }
  
  .modal-details {
    padding: 2rem;
    background: white;
  }
  
  .modal-details h3 {
    color: #1e293b;
    font-size: 1.75rem;
    margin-bottom: 1rem;
  }
  
  .modal-details p {
    color: #64748b;
    line-height: 1.6;
    max-width: 800px;
    margin: 0 auto;
  }
  
  .close-btn {
    position: absolute;
    top: 1rem;
    right: 1rem;
    background: rgba(0, 0, 0, 0.7);
    color: white;
    border: none;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    cursor: pointer;
    font-size: 1.5rem;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .close-btn:hover {
    background: rgba(0, 0, 0, 0.9);
    transform: scale(1.1);
  }
  
  /* @media (max-width: 768px) {
    .service-image-container {
      flex: 0 0 calc(50% - 1rem);
    }
  
    .carousel-track {
      transform: translateX(-${currentSlides[index] * 50}%);
    }
  
    .nav-btn {
      width: 35px;
      height: 35px;
      font-size: 1rem;
    }
  
    .modal-main-image {
      height: 300px;
    }
  } */
  </style>