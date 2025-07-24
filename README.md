# imaitoru
portfolio
import { useState } from "react";
import { motion } from "framer-motion";

const works = [
  {
    id: 1,
    title: "Web Design A",
    category: "Web",
    image: "/images/work1.jpg",
  },
  {
    id: 2,
    title: "Graphic Design B",
    category: "Graphic",
    image: "/images/work2.jpg",
  },
  {
    id: 3,
    title: "Video Project C",
    category: "Video",
    image: "/images/work3.jpg",
  },
  // Add more works here
];

const categories = ["All", "Web", "Graphic", "Video"];

export default function Portfolio() {
  const [selectedCategory, setSelectedCategory] = useState("All");
  const [selectedWork, setSelectedWork] = useState(null);

  const filteredWorks =
    selectedCategory === "All"
      ? works
      : works.filter((w) => w.category === selectedCategory);

  return (
    <div className="min-h-screen bg-gray-100">
      {/* Header */}
      <header className="fixed top-0 left-0 w-full bg-white shadow z-50 p-4 flex justify-between items-center">
        <h1 className="text-xl font-bold">Toru Imai</h1>
        <nav className="space-x-4">
          <a href="#works" className="text-gray-600 hover:text-black">Works</a>
          <a href="#profile" className="text-gray-600 hover:text-black">Profile</a>
          <a href="#contact" className="text-gray-600 hover:text-black">Contact</a>
        </nav>
      </header>

      <main className="pt-20 px-6" id="works">
        {/* Filter Buttons */}
        <div className="flex justify-center space-x-4 mb-6">
          {categories.map((cat) => (
            <button
              key={cat}
              className={`px-4 py-2 rounded-full border ${
                selectedCategory === cat
                  ? "bg-black text-white"
                  : "bg-white text-black"
              }`}
              onClick={() => setSelectedCategory(cat)}
            >
              {cat}
            </button>
          ))}
        </div>

        {/* Works Grid */}
        <div className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6">
          {filteredWorks.map((work) => (
            <div
              key={work.id}
              className="cursor-pointer overflow-hidden rounded-2xl shadow hover:shadow-lg"
              onClick={() => setSelectedWork(work)}
            >
              <img
                src={work.image}
                alt={work.title}
                className="w-full h-64 object-cover"
              />
              <div className="p-4">
                <h3 className="text-lg font-semibold">{work.title}</h3>
                <p className="text-sm text-gray-500">{work.category}</p>
              </div>
            </div>
          ))}
        </div>

        {/* Modal */}
        {selectedWork && (
          <div
            className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50"
            onClick={() => setSelectedWork(null)}
          >
            <motion.div
              layoutId={`work-${selectedWork.id}`}
              className="bg-white rounded-2xl overflow-hidden w-11/12 md:w-2/3 lg:w-1/2 shadow-xl"
              onClick={(e) => e.stopPropagation()}
            >
              <img
                src={selectedWork.image}
                alt={selectedWork.title}
                className="w-full h-[60vh] object-cover"
              />
              <div className="p-6">
                <h2 className="text-2xl font-bold mb-2">{selectedWork.title}</h2>
                <p className="text-gray-600">Category: {selectedWork.category}</p>
              </div>
            </motion.div>
          </div>
        )}
      </main>

      {/* Footer Placeholder */}
      <footer id="contact" className="mt-20 p-6 text-center text-gray-500">
        &copy; {new Date().getFullYear()} Toru Imai
      </footer>
    </div>
  );
}
